My most updated biome configuration as of 2025

## v1 
```json
{
  "$schema": "https://biomejs.dev/schemas/1.0.0/schema.json",
  "vcs": {
		"enabled": true,
		"clientKind": "git",
		"useIgnoreFile": true
	},
	"formatter": {
		"enabled": true,
    "indentStyle": "tab",
    "indentWidth": 2,
    "lineWidth": 90,
    "ignore": ["node_modules", ".next", "dist", ".nuxt", ".wrangler", ".react-email"]
  },
  "javascript": {
    "formatter": {
			"arrowParentheses": "always",
			"quoteStyle": "double",
			"jsxQuoteStyle": "double",
			"bracketSameLine": false,
			"bracketSpacing": true,
			"semicolons": "asNeeded",
			"trailingCommas": "none"
    }
  },
  "json": {
		"formatter": {
			"indentStyle": "tab"
		}
	},

  "linter": {
	  "enable": true,
    "rules": {
	    "recommended": true,
			"correctness": {
				"noUnusedImports": "warn",
				"noUnusedVariables": "warn",
				"noUnsafeOptionalChaining": "error",
				"noUnsafeFinally": "error"
			},
			"nursery": {
				"useSortedClasses": {
					"level": "warn",
					"fix": "safe",
					"options": {
						"attributes": ["className"],
						"functions": ["cn", "clsx", "twMerge"]
					}
				}
			}
    }
  },

	"assist": {
		"enabled": true,
		"actions": {
			"source": {
				"organizeImports": "on"
			}
		}
	}
}
```


## v2 

```json
{
	"$schema": "https://biomejs.dev/schemas/2.0.5/schema.json",
	"vcs": {
		"enabled": true,
		"clientKind": "git",
		"useIgnoreFile": true
	},
	"formatter": {
		"enabled": true,
		"indentStyle": "tab",
		"indentWidth": 2,
		"lineWidth": 90,
		"includes": ["src/**"]
	},
	"javascript": {
		"formatter": {
			"arrowParentheses": "always",
			"quoteStyle": "double",
			"jsxQuoteStyle": "double",
			"bracketSameLine": false,
			"bracketSpacing": true,
			"semicolons": "asNeeded",
			"trailingCommas": "none"
		}
	},
	"json": {
		"formatter": {
			"indentStyle": "tab"
		}
	},

	"linter": {
		"enabled": true,
		"rules": {
			"recommended": true,
			"correctness": {
				"noUnusedImports": "warn",
				"noUnusedVariables": "warn",
				"noUnsafeOptionalChaining": "error",
				"noUnsafeFinally": "error"
			},
			"nursery": {
				"useSortedClasses": {
					"level": "warn",
					"fix": "safe",
					"options": {
						"attributes": ["className"],
						"functions": ["cn", "clsx", "twMerge"]
					}
				}
			}
		}
	},

	"assist": {
		"enabled": true,
		"actions": {
			"source": {
				"organizeImports": "on"
			}
		}
	}
}
```