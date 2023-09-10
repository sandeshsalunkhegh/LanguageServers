# Use the official OpenJDK 17 image as the base image.
FROM openjdk:20-jdk-buster

# Set the working directory in the container.
WORKDIR /app

# Install any required dependencies if needed.

# Download and install the JDTLS JAR file.
RUN wget -L https://github.com/eclipse/eclipse.jdt.ls/archive/refs/tags/v1.26.0.tar.gz
RUN mkdir jdtls
RUN tar -xzf v1.26.0.tar.gz -C jdtls --strip-components=1
RUN rm *.tar.gz
RUN cd jdtls

# Expose the port that the language server will listen on.
# EXPOSE 8080

# Define the command to run the JDTLS.
# CMD ["java", "-jar", "jdtls.jar", "-configuration", "/app/config"]
CMD ["java \
	-Declipse.application=org.eclipse.jdt.ls.core.id1 \
	-Dosgi.bundles.defaultStartLevel=4 \
	-Declipse.product=org.eclipse.jdt.ls.core.product \
	-Dlog.level=ALL \
	-Xmx1G \
	--add-modules=ALL-SYSTEM \
	--add-opens java.base/java.util=ALL-UNNAMED \
	--add-opens java.base/java.lang=ALL-UNNAMED \
	-jar ./plugins/org.eclipse.equinox.launcher_1.5.200.v20180922-1751.jar \
	-configuration ./config_linux \
	-data /path/to/data"]

# Define the command to run the JDTLS.
# CMD ["java", \
#     "-Declipse.application=org.eclipse.jdt.ls.core.id1", \
#     "-Dosgi.bundles.defaultStartLevel=4", \
#     "-Declipse.product=org.eclipse.jdt.ls.core.product", \
#     "-Dlog.level=ALL", \
#     "-Xmx1G", \
#     "--add-modules=ALL-SYSTEM", \
#     "--add-opens java.base/java.util=ALL-UNNAMED", \
#     "--add-opens java.base/java.lang=ALL-UNNAMED", \
#     "-jar", \
#     "./jdtls/plugins/org.eclipse.equinox.launcher_1.5.200.v20180922-1751.jar", \
#     "-configuration", \
#     "./jdtls/config_linux", \
#     "-data", \
#     "/path/to/data"]
