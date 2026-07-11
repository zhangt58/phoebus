# Display Builder Product

This curated Phoebus product selects only the Display Builder (`app-display-editor`)
and Display Runtime (`app-display-runtime`) applications. It also includes the
launcher, display fonts, and Channel Access/PV Access providers needed for normal
display operation.

Some non-application libraries from Data Browser and 3D Viewer remain transitive
requirements of the built-in Display Builder widget representations. Other Phoebus
applications are not selected by this product.

Build the product and only its reactor dependencies with:

```sh
mvn install -DskipTests -f dependencies/install-jars/pom.xml
mvn install -DskipTests -Djavafx.platform=mac-aarch64 \
  -pl phoebus-product-display -am
```

The first command installs repository-bundled dependencies, such as
`org.epics:pbrawclient`, into the local Maven repository. These artifacts are
required transitively by the built-in Data Browser display widgets and are not
available from Maven Central.

The distributable archive is written to `phoebus-product-display/target/`.
