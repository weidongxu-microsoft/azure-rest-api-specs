# GitHub Copilot Instructions for Azure REST API Specs

This document provides guidance for using GitHub Copilot effectively with the Azure REST API Specifications repository.

## Common Tasks

### Adding or Modifying TypeSpec Configurations for Java

When adding or modifying emitter configurations in TypeSpec projects:

1. Locate the `tspconfig.yaml` file in the service directory.
2. Configure options in the `options` section, but DO NOT modify `emit` section:
   ```yaml
   options:
     "@azure-tools/typespec-java":
       package-dir: "azure-resourcemanager-<servicename>"
       service-name: "<Service Name>"
       flavor: "azure"
   ```
3. Locate or create the `client.tsp` file in the service directory
4. Make sure imports is correct.
   ```tsp
   import "./main.tsp";
   import "@azure-tools/typespec-client-generator-core";

   using Azure.ClientGenerator.Core;
   ```
5. Add a `@@clientName(<typespecnamespace>, "<ServiceNameManagementClient>", "java");`; for `<typespecnamespace>` check namespace in `main.tsp`, it contains no quote.
6. Add a `@@clientNamespace(<typespecnamespace>, "com.azure.resourcemanager.<servicename>", "java");`.
7. run `npx tsv <path-to-service>` to format the files.

## Best Practices

1. Follow the established patterns in the repository for naming and file structure
2. Use the appropriate TypeSpec decorators to ensure consistent naming across languages
3. Keep the configuration for each language consistent with other services
4. Ensure all required emitters are properly configured in the tspconfig.yaml file
5. Use clientNamespace decorators to specify language-specific namespaces

## Documentation References

- [Getting Started with TypeSpec Specifications](./documentation/Getting-started-with-TypeSpec-specifications.md)
- [TypeSpec Structure Guidelines](./documentation/typespec-structure-guidelines.md)
- [TypeSpec REST API Development Process](./documentation/typespec-rest-api-dev-process.md)