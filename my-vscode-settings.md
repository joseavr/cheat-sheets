## Settings - June 2025

```json
{
	// console ninja extension
	"console-ninja.featureSet": "Community",

	// scope highlighter extension
	"codeScopeHighlighter.bracketColor": "#dc2626dd",

	// react-snippets extension
	"reactSnippets.settings.importReactOnTop": false,

	// template string extension
	"template-string-converter.quoteType": "double",
	"template-string-converter.autoRemoveTemplateString": true,
	"template-string-converter.convertOutermostQuotes": true,

	// project-manager extension
	"projectManager.git.baseFolders": [
		"\\\\wsl.localhost\\Ubuntu\\home\\jvaldiv8\\CMSC330\\projects",
		"C:\\Users\\pjose\\Documents",
		"/Users/jvaldiv8/pr"
	],

	// biome extension
	"editor.defaultFormatter": "biomejs.biome",

	// extensions settings
	"extensions.ignoreRecommendations": true,
	"biome.suggestInstallingGlobally": false,

	// language settings
	"javascript.updateImportsOnFileMove.enabled": "always",
	"typescript.updateImportsOnFileMove.enabled": "always",
	"[python]": {
		"editor.formatOnType": true
	},
	"[html]": {
		"editor.defaultFormatter": "vscode.html-language-features"
	},

	// git
	"git.autofetch": true,
	"git.confirmSync": false,
	"git.openRepositoryInParentFolders": "never",
	"diffEditor.renderSideBySide": false,

	// inline suggestion
	"editor.inlineSuggest.enabled": true,
	"emmet.triggerExpansionOnTab": true,
	"emmet.useInlineCompletions": true,
	"editor.suggest.showWords": false,
	"editor.suggest.showKeywords": false,
	"editor.parameterHints.enabled": false,
	"editor.hover.enabled": true,
	"editor.acceptSuggestionOnEnter": "on",
	"editor.quickSuggestions": {
		"other": "off", // wont appear suggestion as you type
		"comments": "off",
		"strings": "off"
	},

	// file explorer settings
	"explorer.confirmDelete": false,
	"explorer.confirmDragAndDrop": false,
	"workbench.tree.renderIndentGuides": "onHover",
	"workbench.tree.indent": 16,
	"workbench.tree.enableStickyScroll": true,

	// markdown
	"markdown.preview.typographer": true,
	"markdown.preview.scrollPreviewWithEditor": false,

	// file Nesting
	"explorer.fileNesting.enabled": true,
	"explorer.fileNesting.patterns": {
		"*.ts": "${capture}.test.ts",
		"*.js": "${capture}.js.map, ${capture}.min.js, ${capture}.d.ts, ${capture}.test.js",
		"package.json": "package-lock.json, yarn.lock, pnpm-lock.yaml, bun.lockb, *.config.js, *.config.ts, *.config.cjs, *.config.mjs , *.json, .*, *.ts"
	},

	// terminal
	"terminal.integrated.env.osx": {
		"FIG_NEW_SESSION": "1"
	},
	"terminal.integrated.gpuAcceleration": "on",
	"terminal.integrated.defaultProfile.windows": "Git Bash",
	"terminal.integrated.env.windows": {},
	"terminal.integrated.scrollback": 3000,
	"terminal.integrated.smoothScrolling": true,
	"terminal.integrated.enableMultiLinePasteWarning": "never",

	// fonts
	"editor.fontLigatures": true,
	"terminal.integrated.fontFamily": "Cascadia Code PL, JetBrainsMono Nerd Font, MesloLGS NF, Roboto Mono",
	"terminal.integrated.fontSize": 14,
	"terminal.integrated.lineHeight": 1.2,
	"terminal.integrated.fontWeight": "500",
	// "terminal.integrated.letterSpacing": 1,
	"editor.fontFamily": "Cascadia Code PL, MesloLGS NF, JetBrainsMono Nerd Font, Geist Mono, Menlo, Monaspace Argon",
	"editor.fontSize": 12,
	"editor.lineHeight": 1.5,
	"editor.fontWeight": "500",
	// "editor.letterSpacing": 0.2,
	"editor.wordWrap": "on",
	"window.zoomLevel": 1,
	
	// editor theme
	"workbench.colorTheme": "Pitch Black",
	"workbench.preferredDarkColorTheme": "Pitch Black",
	"workbench.preferredLightColorTheme": "GitHub Light Default",
	// theme by Dark/Light
	"workbench.colorCustomizations": {
		"[Blue Moon theme]": {
			//** color for dark
			"editor.lineHighlightBackground": "#0b0b0ba9",
			"tab.activeBorder": "#4c8bf0e5",
			"tab.activeBorderTop": "#4c8bf000", // tab top border
			"tab.border": "#ffffff00",
			"titleBar.activeBackground": "#14181f",
			"window.activeBorder": "#004dc1",
			"window.inactiveBorder": "#032b6689",
			"editorIndentGuide.background1": "#01052902",
			"editorIndentGuide.activeBackground1": "#da3d77f1"
			//** spotlight
			// ,"quickInput.background": "#14181f8f" // BACKGROUND
		},
		"[Pitch Black]": {
			// "editor.lineHighlightBackground": "#0b0b0ba9", // cursor line highlight
			"tab.activeBorder": "#4c8bf0e5", // active tab bottom color
			"editorIndentGuide.background1": "#01052902",
			"editorIndentGuide.activeBackground1": "#da3d77f1"
		},
		"[GitHub Light Default]": {
			//
		}
	},
	// "editor.tokenColorCustomizations": {
	//   "comments": {
	//     "fontStyle": "italic",
	//     "foreground": "#9b979778"
	//   }
	// },

	// editor settings
	"explorer.confirmPasteNative": false,
	"editor.suggest.insertMode": "replace",
	"editor.formatOnSave": true,
	"editor.accessibilitySupport": "off",
	"editor.screenReaderAnnounceInlineSuggestion": false,
	"editor.stickyScroll.enabled": true,
	"editor.acceptSuggestionOnCommitCharacter": false,
	"editor.tabCompletion": "on",
	"editor.renderLineHighlightOnlyWhenFocus": true,
	"editor.scrollBeyondLastLine": false,
	"editor.defaultColorDecorators": "auto",
	"editor.renderLineHighlight": "all",
	"editor.guides.bracketPairsHorizontal": false,
	"editor.guides.bracketPairs": "active",
	"editor.matchBrackets": "never",
	"editor.cursorBlinking": "solid",
	"editor.cursorWidth": 2,
	"editor.cursorStyle": "block",
	"editor.cursorSurroundingLines": 5,
	"editor.cursorSmoothCaretAnimation": "off",
	"json.schemaDownload.enable": true,

	// editor ui
	"window.customTitleBarVisibility": "never",
	"breadcrumbs.enabled": false,
	"workbench.list.smoothScrolling": true,
	"editor.smoothScrolling": true,
	"editor.tabSize": 2,
	"editor.renderWhitespace": "none",
	"symbols.hidesExplorerArrows": false, // deprecated
	"workbench.sideBar.location": "right",
	"workbench.layoutControl.enabled": false,
	"editor.minimap.enabled": false,
	"editor.glyphMargin": true,
	"window.commandCenter": false,
	"window.zoomLevel": 0,
	"workbench.activityBar.location": "default",
	"explorer.compactFolders": false,
	"workbench.iconTheme": "symbols",
	"window.titleBarStyle": "native",
	"custom-ui-style.electron": {
		"titleBarStyle": "hiddenInset",
		"trafficLightPosition": {
			"x": -100,
			"y": 70
		}
	},
	"custom-ui-style.external.imports": [
		"file:///Users/jvaldiv8/vscode-styles-cursor.css"
	],
	"custom-ui-style.stylesheet": {
		// move tabs to the right
		//  ".monaco-workbench .part.editor > .content .editor-group-container > .title .tabs-container > div:first-child": "padding-left: 100px",

		// tabs same theme color
		".title.tabs.show-file-icons": "background-color: var(--vscode-editor-background) !important",

		// right panel same theme color
		".split-view-container > .visible": "background-color: var(--vscode-editor-background) !important;",

		// animation on bottom statusbar
		".statusbar": "opacity: 0.3; transition: 0.3s ease-in-out",
		".statusbar:hover": "opacity: 1",

		// comments font
		// ".mtk14": "font-family: 'Monaspace Radon' !important; font-size: 14px !important",

		// scrollbar
		".find-widget": "border-radius:6px; backdrop-filter:blur(10px);",
		".monaco-inputbox, .scm-editor": "border-radius:6px !important;",
		".slider": "width: 6px !important; border-radius: 16px;",
		".monaco-button-dropdown": "border-radius:6px !important;",

		// testing options
		".notification-toast": "backdrop-filter:blur(10px); border: 1px solid #ffffff09 !important; border-radius: 8px !important; ",

		// fix editor color when using command pallete with blur
		"body .monaco-workbench": "--al-transparency-percent: 25%; --al-tab-height: 46px; --al-tab-y-offset: 7px; --al-command-palette-blur-amount: 2px; --al-tab-fontSize: 14px;",
		".tab-border-bottom-container": "height: 1.5px !important"
	},
}
```


## Settings for React Profile - June 2025

```json
{
	// console ninja extension
	"console-ninja.featureSet": "Community",

	// scope highlighter extension
	"codeScopeHighlighter.bracketColor": "#dc2626dd",

	// react-snippets extension
	"reactSnippets.settings.importReactOnTop": false,

	// template string extension
	"template-string-converter.quoteType": "double",
	"template-string-converter.autoRemoveTemplateString": true,
	"template-string-converter.convertOutermostQuotes": true,

	// project-manager extension
	"projectManager.git.baseFolders": [
		"\\\\wsl.localhost\\Ubuntu\\home\\jvaldiv8\\CMSC330\\projects",
		"C:\\Users\\pjose\\Documents",
		"/Users/jvaldiv8/pr"
	],

	// biome extension
	"editor.defaultFormatter": "biomejs.biome",

	// extensions settings
	"extensions.ignoreRecommendations": true,
	"biome.suggestInstallingGlobally": false,

	// language settings
	"javascript.updateImportsOnFileMove.enabled": "always",
	"typescript.updateImportsOnFileMove.enabled": "always",
	"[python]": {
		"editor.formatOnType": true
	},
	"[html]": {
		"editor.defaultFormatter": "vscode.html-language-features"
	},

	// git
	"git.autofetch": true,
	"git.confirmSync": false,
	"git.openRepositoryInParentFolders": "never",
	"diffEditor.renderSideBySide": false,

	// inline suggestion
	"editor.inlineSuggest.enabled": true,
	"emmet.triggerExpansionOnTab": true,
	"emmet.useInlineCompletions": true,
	"editor.suggest.showWords": false,
	"editor.suggest.showKeywords": false,
	"editor.parameterHints.enabled": false,
	"editor.hover.enabled": true,
	"editor.acceptSuggestionOnEnter": "on",
	"editor.quickSuggestions": {
		"other": "off", // wont appear suggestion as you type
		"comments": "off",
		"strings": "off"
	},

	// file explorer settings
	"explorer.confirmDelete": false,
	"explorer.confirmDragAndDrop": false,
	"workbench.tree.renderIndentGuides": "onHover",
	"workbench.tree.indent": 16,
	"workbench.tree.enableStickyScroll": true,

	// markdown
	"markdown.preview.typographer": true,
	"markdown.preview.scrollPreviewWithEditor": false,

	// file Nesting
	"explorer.fileNesting.enabled": true,
	"explorer.fileNesting.patterns": {
		"*.ts": "${capture}.test.ts",
		"*.js": "${capture}.js.map, ${capture}.min.js, ${capture}.d.ts, ${capture}.test.js",
		"package.json": "package-lock.json, yarn.lock, pnpm-lock.yaml, bun.lockb, *.config.js, *.config.ts, *.config.cjs, *.config.mjs , *.json, .*, *.ts"
	},

	// terminal
	"terminal.integrated.env.osx": {
		"FIG_NEW_SESSION": "1"
	},
	"terminal.integrated.gpuAcceleration": "on",
	"terminal.integrated.defaultProfile.windows": "Git Bash",
	"terminal.integrated.env.windows": {},
	"terminal.integrated.scrollback": 3000,
	"terminal.integrated.smoothScrolling": true,
	"terminal.integrated.enableMultiLinePasteWarning": "never",

	// fonts
	"editor.fontLigatures": false,
	"terminal.integrated.fontFamily": "Cascadia Code PL, JetBrainsMono Nerd Font, MesloLGS NF, Roboto Mono",
	"terminal.integrated.fontSize": 14,
	"terminal.integrated.lineHeight": 1.2,
	"terminal.integrated.fontWeight": "500",
	// "terminal.integrated.letterSpacing": 1,
	"editor.fontFamily": "Cascadia Code PL, MesloLGS NF, JetBrainsMono Nerd Font, Geist Mono, Menlo, Monaspace Argon",
	"editor.fontSize": 12,
	"editor.lineHeight": 1.5,
	"editor.fontWeight": "500",
	// "editor.letterSpacing": 0.2,
	"editor.wordWrap": "on",
	"window.zoomLevel": 1,
	
	// editor theme
	"workbench.colorTheme": "Pitch Black",
	"workbench.preferredDarkColorTheme": "Pitch Black",
	"workbench.preferredLightColorTheme": "GitHub Light Default",
	// theme by Dark/Light
	"workbench.colorCustomizations": {
		"[Blue Moon theme]": {
			//** color for dark
			"editor.lineHighlightBackground": "#0b0b0ba9",
			"tab.activeBorder": "#4c8bf0e5",
			"tab.activeBorderTop": "#4c8bf000", // tab top border
			"tab.border": "#ffffff00",
			"titleBar.activeBackground": "#14181f",
			"window.activeBorder": "#004dc1",
			"window.inactiveBorder": "#032b6689",
			"editorIndentGuide.background1": "#01052902",
			"editorIndentGuide.activeBackground1": "#da3d77f1"
			//** spotlight
			// ,"quickInput.background": "#14181f8f" // BACKGROUND
		},
		"[Pitch Black]": {
			// "editor.lineHighlightBackground": "#0b0b0ba9", // cursor line highlight
			"tab.activeBorder": "#4c8bf0e5", // active tab bottom color
			"editorIndentGuide.background1": "#01052902",
			"editorIndentGuide.activeBackground1": "#da3d77f1",
		},
		"[GitHub Light Default]": {
			//
		}
	},
	// "editor.tokenColorCustomizations": {
	//   "comments": {
	//     "fontStyle": "italic",
	//     "foreground": "#9b979778"
	//   }
	// },

	// editor settings
	"explorer.confirmPasteNative": false,
	"editor.suggest.insertMode": "replace",
	"editor.formatOnSave": false,
	"editor.accessibilitySupport": "off",
	"editor.screenReaderAnnounceInlineSuggestion": false,
	"editor.stickyScroll.enabled": true,
	"editor.acceptSuggestionOnCommitCharacter": false,
	"editor.tabCompletion": "on",
	"editor.renderLineHighlightOnlyWhenFocus": true,
	"editor.scrollBeyondLastLine": false,
	"editor.defaultColorDecorators": "auto",
	"editor.renderLineHighlight": "all",
	"editor.guides.bracketPairsHorizontal": false,
	"editor.guides.bracketPairs": "active",
	"editor.matchBrackets": "never",
	"editor.cursorBlinking": "solid",
	"editor.cursorWidth": 2,
	"editor.cursorStyle": "block",
	"editor.cursorSurroundingLines": 20,
	"editor.cursorSmoothCaretAnimation": "off",
	"json.schemaDownload.enable": true,

	// editor ui
	"editor.rulers": [ {
		"column": 90,    // vertical ruler
		"color": "#212120"
	}],
	"workbench.panel.showLabels": false,
	"window.customTitleBarVisibility": "never",
	"breadcrumbs.enabled": false,
	"workbench.list.smoothScrolling": true,
	"editor.smoothScrolling": true,
	"editor.tabSize": 2,
	"editor.renderWhitespace": "none",
	"symbols.hidesExplorerArrows": false, // deprecated
	"workbench.sideBar.location": "right",
	"workbench.layoutControl.enabled": false,
	"editor.minimap.enabled": false,
	"editor.glyphMargin": true,
	"window.commandCenter": false,
	// "window.zoomLevel": 0,
	"workbench.activityBar.location": "default",
	"explorer.compactFolders": false,
	"workbench.iconTheme": "symbols"
}
```


## Settings attached to a project - June 2025

```json
{
	"editor.tabSize": 2,

	"git.autofetch": true,

	"explorer.fileNesting.enabled": true,
	"explorer.fileNesting.patterns": {
		"*.ts": "${capture}.test.ts",
		"*.js": "${capture}.js.map, ${capture}.min.js, ${capture}.d.ts, ${capture}.test.js",
		"package.json": "package-lock.json, yarn.lock, pnpm-lock.yaml, bun.lockb, *.config.js, *.config.ts, *.config.cjs, *.config.mjs , *.json, .*, *.ts"
	},

	"editor.codeActionsOnSave": {
		"source.addMissingImports.ts": "explicit",
		"quickfix.biome": "explicit",
		"source.organizeImports.biome": "explicit",
		"source.fixAll.biome": "explicit"
	},
	"notebook.codeActionsOnSave": {
		"quickfix.biome": "explicit"
	},

	"editor.suggest.insertMode": "replace",

	"editor.defaultFormatter": "biomejs.biome",
	"diffEditor.ignoreTrimWhitespace": false,
	"editor.formatOnSave": true,
	"editor.formatOnPaste": false,

	"files.insertFinalNewline": true,

	"typescript.validate.enable": true,

	"javascript.validate.enable": true,

	"[javascript][javascriptreact][typescript][typescriptreact][json][css][tailwindcss]": {
		"editor.defaultFormatter": "biomejs.biome"
	}
}

```