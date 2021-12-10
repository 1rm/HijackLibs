# YAML Schema
A formal version of the below can be found [here](.github/schema/schema.yml).
| Field | Type | Required | Format | Description |
| ----- | ---- | -------- | ------ | ----------- |
| `Name`| String | ✅ | All lower case, must end in `.dll` | Name of the DLL that is being recorded. |
| `Author` | String | ✅ | N/A | Full name of the person creating the entry. | 
| `Created` | Date| ✅ | YYYY-MM-DD | Date of when the entry was first created. |
| `Vendor` | String | ✅ | N/A | Name of the vendor providing the DLL. | 
| `CVE` | String | Optional | CVE-YYYY-XXXX | ID of the assigned CVE, if applicable. |
| `ExpectedLocations` | List[String] | Optional | No trailing slashes | Folder locations[^1] where legitimate versions of the DLL are normally found. |
| `VulnerableExecutables` | List[[VulnerableExecutable](#VulnerableExecutable)] | ✅ | N/A | Executables that are known to load the DLL described. | 
| `Resources` | List[String] | Optional | HTTP(S) links only | URLs to relevant content that may explain further context (e.g. a PDF report, a tweet, a YouTube video).|
| `Acknowledgements` | List[[Acknowledgement](#Acknowledgement)] | Optional | N/A | People who should be acknowledge for finding this entry (i.e. who did the actual research). |

## VulnerableExecutable
| Field | Type | Required | Format | Description |
| ----- | ---- | -------- | ------ | ----------- |
| `Path` | String | ✅ | Has to end in .exe | Full location[^1] of legitimate executables that attempt to load the described DLL. |
| `Type` | String | ✅ | `Sideloading` \| `Phantom` \| `Search Order` | The type of DLL Hijacking this executable is vulnerable to. |
| `AutoElevate` | Boolean | Optional | `true` only | Only create this field and set to `true` if the executable is automatically elevated by Windows. |
| `PrivilegeEscalation` | Boolean | Optional | `true` only | Only create this field and set to `true` if the executable normally runs under elevated privileges. |
| `Condition` | String | Optional | N/A | If certain conditions are required for the attack to work, you can state them here. |
| `SHA256` | List[String] | Optional | 64 characters | If the executable is 3rd-party (i.e. non-Microsoft), please add the SHA256 hash of the executable here. |

## Acknowledgement
| Field | Type | Required | Format | Description |
| ----- | ---- | -------- | ------ | ----------- |
| `Name` | String | ✅ | N/A | Full name (or Twitter screen name) of the person who should be acknowledged. | 
| `Twitter` | String | Optional | Has to start with `@` | The Twitter handle of the person who should be acknowledged. | 

[^1]: This field supports environment variables such as `%SYSTEM32%`, `%SYSWOW64%`, `%PROGRAMFILES%`, `%PROGRAMFILES(x86)%`, `%PROGRAMDATA%`, `%APPDATA%`, and so on. Please use this where possible. Variable `%VERSION%` is also available if a path contains a version number that is likely to change. 