## Java

```yaml
security: AADToken
security-scopes: https://communication.azure.com//.default

tag: package-phonenumber-2021-03-07

output-folder: $(java-sdks-folder)/sdk/communication/azure-communication-phonenumbersdemo
data-plane: true
namespace: com.azure.communication.phonenumbersdemo

partial-update: true

service-name: PhoneNumbers
service-versions:
  - '2021-03-07'

generate-samples: true
generate-tests: true

polling:
  PhoneNumbers_SearchAvailablePhoneNumbers:
    strategy: new com.azure.communication.phonenumbersdemo.implementation.PhoneNumbersSearchPollingStrategy<>(this, {httpPipeline}, null, {context})
    intermediate-type: com.azure.communication.phonenumbersdemo.models.PhoneNumberOperation
    final-type: com.azure.communication.phonenumbersdemo.models.PhoneNumberSearchResult

generate-models: true
custom-types: BillingFrequency,PhoneNumberAssignmentType,PhoneNumberCapabilities,PhoneNumberCapabilityType,PhoneNumberCost,PhoneNumberOperationStatus,PhoneNumberOperationType,PhoneNumberSearchResult,PhoneNumberType
custom-types-subpackage: models
```
