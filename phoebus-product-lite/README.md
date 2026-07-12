# Phoebus Lite Product

This curated Phoebus product selects the Display Builder (`app-display-editor`),
Display Runtime (`app-display-runtime`), and all Debug applications from the full
product: Diagnostics and Formula Tree (`app-diag`), Error Log (`app-errlog`), and
Performance Monitor (`app-perfmon`). Debug tools supplied directly by `core-ui`,
such as Jobs, PV List, and Freeze UI, are included transitively. The product also
includes the launcher, display fonts, and Channel Access/PV Access providers needed
for normal display operation. PV Table (`app-pvtable`) and PV Tree (`app-pvtree`)
are included as additional process-variable display applications.

Some non-application libraries from Data Browser and 3D Viewer remain transitive
requirements of the built-in Display Builder widget representations. Other Phoebus
applications are not selected by this product.

Build the product and only its reactor dependencies with:

```sh
mvn install -DskipTests -f dependencies/install-jars/pom.xml
mvn install -DskipTests -Djavafx.platform=mac-aarch64 \
  -pl phoebus-product-lite -am
```

The first command installs repository-bundled dependencies, such as
`org.epics:pbrawclient`, into the local Maven repository. These artifacts are
required transitively by the built-in Data Browser display widgets and are not
available from Maven Central.

The distributable archive is written to `phoebus-product-lite/target/` using
the original product filename, `product-<version>.tar.gz`.

When a GitHub Release is published, the release workflow performs native builds
and uses `jpackage` to create self-contained ARM64 macOS (`.pkg`), Windows x64
(`.exe`), and Linux x64 (`.deb`) installers named `CS-Studio`. Each installed
application uses `core/ui/src/main/resources/icons/phoebus-logo.png` as its app
and installer icon; the workflow converts it to `.icns` and `.ico` where required.
The unsigned installers and the macOS product archive are attached to the release.
