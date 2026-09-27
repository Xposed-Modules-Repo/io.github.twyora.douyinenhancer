# Custom Obfuscation Mapping

This section describes how to import an obfuscation mapping to attempt restoring module
functionality when the built-in obfuscated method lookup rules stop working.

## About the Module Obfuscation Mapping

The module obfuscation mapping decouples the logical names used in hook logic from the obfuscated
names in the host app code.
After the host app updates, if the underlying method logic has not changed significantly, the module
can keep working as long as the method names in the new obfuscation mapping correctly match those of
the current host version.

## Purpose of This Feature

When adapting to new host app versions, most effort goes into adjusting the module’s built-in lookup
rules to match host code logic, while the high-level hook logic rarely needs changes.
The maintainer acknowledges that perfect lookup rules that work reliably across all host versions
cannot be written.
Moreover, **if the module stops working merely because host app updates break method lookup**,
waiting for the maintainer to update lookup rules introduces significant delays and leaves features
unusable for a long time.

Custom obfuscation mapping is designed to address exactly this scenario: it lets you manually fill
in missing method mappings to quickly restore functionality without waiting for maintainer updates.

## Structure of Custom Obfuscation Mapping

Below is an obfuscation mapping template:

```json
{
  "hookInfo": {
    // All three fields below are optional and limit the scope where this configuration applies.
    // Strongly recommended to fill them out. If omitted, the module ignores these constraints,
    // which may cause the configuration to load on the wrong version and crash the module or host app!
    "module_version_code": "<moduleVersionCode>",
    "module_version_name": "<moduleVersionName>",
    "host_version_code": "<hostVersionCode>",
    "<class_name>": {
      "class": {
        "name": "<classQualifiedName>"
      },
      "<method_name>": {
        "name": "<methodName>",
        "parameters": {
          "values": [
            // When overloaded versions exist, locate the method required by the module according to the parameter order in the function signature.
            // If the list is empty, match only by method name.
            "<paramTypeQualifiedName>",
            ...
          ]
        }
      },
      "<field_name>": {
        "name": "<fieldName>"
      }
    },
    ...
  },
  // Optional. Distinguishes official configurations from user custom ones.
  // Missing or invalid signature will not block import.
  "signature": "..."
}
```

> The `hookInfo` in custom mappings will be **merged with the internally generated `hookInfo` using
override semantics**: explicitly specified fields override their corresponding generated values,
> while unspecified fields retain the built-in results unchanged.
>
> For example, if only `hookInfo.<class_name>.<method_name>.name` is set without configuring its
`<parameters>.values`, after merging, the method name will use the explicitly defined value, and the
> parameter list will continue to use the internally generated result.

**Notice**: Although custom obfuscation mapping contains a signature field, import will not be
rejected even if signature verification fails.
Loading an incorrect mapping may break module functionality or even crash the module and host app.
Therefore, if you have imported an unsigned obfuscation mapping before clearing the custom
obfuscation mapping, you automatically forfeit the right to submit bug reports to the maintainer,
**unless you can clearly and immediately prove that the imported mapping has no connection
whatsoever
to your reported bug**.

Examples of valid exceptions:

1. Importing the custom obfuscation mapping failed, or the mapping did not take effect.
2. Module functionality remains unrecoverable even after importing a correctly written mapping.
3. The feature related to your bug report does not use any entries from the custom obfuscation
   mapping you imported.

>
> In future releases, users will be able to submit custom obfuscation mappings to the module.
> Maintainers may review and sign these mappings, so other users can select and load them as needed.

## Steps to Use Custom Obfuscation Mapping

>
> If your module works properly, there is no need to load a custom obfuscation mapping.

1. Check the obfuscation mapping logs printed by the module early in the host app lifecycle to
   identify fields that failed lookup.
2. Refer to the built-in obfuscated method lookup rules in the module source code, and find the
   actual field names for your host app version.
3. Import your self-written obfuscation mapping.

>
> If the import succeeds but module functionality still cannot be restored while the custom mapping
> is confirmed active, submit a bug report to the maintainer.
