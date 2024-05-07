# pkl-strings

Generate platform specific string/translation files from a single source file. Currently supports iOS and Android.

## Usage
![Stable](https://img.shields.io/github/v/release/BenMMcLean/pkl-strings?label=Stable)
![Preview](https://img.shields.io/github/v/release/BenMMcLean/pkl-strings?label=Preview&include_prereleases)

Make a new source file amending `strings.pkl` and override `localizable`:
```pkl
amends "package://benm.cl/pkl-strings/pkl-strings@<version>/pkl-strings@<version>.zip"

localizable = new Localizable {
    languages = new Listing {
        new Language {
            code = "en"
            strings = new Listing {
                new SingleResourceString {
                    name = "single"
                    value = "TestValue"
                },
                new QuantityResourceString {
                    name = "quantity_positional"
                    options = new Listing {
                        new QuantityOption {
                            quantity = "one"
                            value = "%d Thing"
                        }
                        new QuantityOption {
                            quantity = "other"
                            value = "%d Things"
                        }
                    }
                }
            }
        }
    }
}
```

This file can then be exported as an Android `strings.xml` and iOS `Localizable.xcstrings` using the command
```bash
pkl eval file.pkl -m .
```

This will automatically render the localized strings into an `android` and `apple` directory for Android strings and iOS strings respectively.