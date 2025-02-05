# Changelog

## [insiders] (master)

Note: Can be used using `nvuillam/mega-linter@insiders` in your GitHub Action mega-linter.yml file, or with `nvuillam/mega-linter@latest` docker image

- Linter versions upgrades
  - None yet !
<!-- linter-versions-end -->

## [4.23.0] 2021-01-12

- Core
  - If the linter is a formatter, errors are not considered as blocking errors by default

- Linters
  - Add **prettier** to format Javascript and Typescript. **standard** remains default
  - Add **remark-lint** to check and fix Markdown files. **markdownlint** remains default

- Linter versions upgrades
  - [golangci-lint](https://golangci-lint.run/) from 1.35.0 to **1.35.1** on 2021-01-11
    - [golangci-lint](https://golangci-lint.run/) from 1.35.1 to **1.35.2** on 2021-01-11
    - [golangci-lint](https://golangci-lint.run/) from 1.34.1 to **1.35.0** on 2021-01-08
  - [cfn-lint](https://github.com/martysweet/cfn-lint) from 0.44.2 to **0.44.3** on 2021-01-09
  - [tflint](https://github.com/terraform-linters/tflint) from 0.23.0 to **0.23.1** on 2021-01-10
  - [dotenv-linter](https://dotenv-linter.github.io/) from 2.2.1 to **3.0.0** on 2021-01-11
    - Update Mega-Linter to call dotenv-linter v3 with `fix` and not `--fix` anymore
  - [phpstan](https://phpstan.org/) from 0.12.65 to **0.12.66** on 2021-01-11

## [4.22.1] 2021-01-07

- Core
  - Improve `warning` status in logs
  - Remove timestamp at each log line

- Enhance integration with GitLab CI
  - Update configuration generator
  - Update core to clean logs when in GitLab CI context

## [4.22.0] 2021-01-06

- Core
  - Allow user to configure custom scripts in `.mega-linter.yml` to run before and after linting, with variables `PRE_RUN` and `POST_RUN`
  - Fix wrong linter status bug
  - Enhance configuration variables performances
  - Rename XXX_FILE_NAME into XXX_CONFIG_FILE

- Linters
  - Add JSONC (json with comments) linting with eslint-plugin-jsonc

## [4.21.0] 2021-01-03

- Linters
  - Add misspell spell checker
  - Allow to define cli_lint_errors_regex in descriptors to extract number of errors from linter output stdout
  - Call linters CLIs with list of files instead of once by file, to improve performances
    - eslint
    - markdownlint
    - pylint
    - flake8
    - isort

- Core
  - Implement architecture for Mega-Linter plugins
  - Count number of errors in linter logs with regexes (`cli_lint_errors_count` and `cli_lint_errors_regex` in descriptor files)
  - Cleanup unused legacy from Super-Linter

- Reports
  - Better icons for Console, GitHub Comment and Text reporters: ✅ ❌

- Documentation
  - Add Install button for VsCode IDE extensions when available
  - Add Install button for JetBrains IDEs extensions when available
  - Add a new page **All linters** listing all linters and references to Mega-Linter in their documentation
  - Add json-schema documentation generation and references

- CI
  - Use `quick build` and `TEST_KEYWORDS` in commit messages, to improve contributor experience

- Fixes
  - Upgrade .tflint default config to work with new tflint version

## [4.20.0] 2020-12-28

- Flavors
  - Add **ci_light** flavor for only CI config files (Dockerfile,Jenkinsfile,JSON,YAML,XML)
  - Add **salesforce** flavor for Salesforce projects (DX or Metadata)
  - If all required linters are not in the current flavor, just skip them with a warning message

- Core
  - Add Json Schema for descriptors (allows validation and auto-completion from IDEs)
  - Add Json Schema for .mega-linter.yml configuration files

## [4.19.0] 2020-12-27

- Installation
  - Add a yeoman generator in mega-linter-runner to initialize configuration in a repository: `npx mega-linter-runner --install`

- Linters
  - New linter v8r to validate json and yaml files with schemastore.org

## [4.18.0] 2020-12-23

- Core
  - Do not suggest flavors when Mega-Linter validates only the diff files (`VALIDATE_ALL_CODE_BASE: false`)
  - Fix ConsoleReporter active linters table content
  - Check if linter is able to fix before flagging it as a fixing linter during runtime

- Flavors
  - New flavor: **documentation**

- Reporters
  - Support GitHub Enterprise for GitHub Comment Reporter
  - Support GitHub Enterprise for GitHub Status Reporter

- Doc
  - Add docker pulls badge in flavors documentation
  - Generate list of references to Mega-Linter

## [4.17.0] 2020-12-18

- Core
  - Allow to use remote linters configuration files with LINTER_RULES_PATH
  - Add `.jekyll-cache` in the list of ignored folders by default
  - Arrange display of Flavor suggestions (text and order) in reporter logs
- Build
  - Dynamically generate (build.py) the list of flavors in github actions workflows
- Doc
  - Reorganize online documentation menus
- Linters
  - Add new linter git_diff to check for git conflicts markers
  - Fix rakudo installation
  - Fix phpstan installation

## [4.16.0] 2020-12-14

- Flavored Mega-Linters
  - Generate lightweight docker images to improve Mega-Linter performances on some language based projects
  - During Mega-Linter run, suggest user to use a flavor and write it in reporters
  - Update descriptor YML files to define flavours
  - Update build.py to create one Dockerfile by Mega-Linter flavour & flavors documentation
  - New GHA workflows to build all flavoured Mega-Linters when pushing in master

- Fixes
  - Output reporter problems as warnings
  - Do not make Mega-Linter fail in case GitHubStatusReporter fails

- Doc
  - Rename "index" pages into more meaningful labels

## [4.15.0] 2020-12-13

- Add Vue.js linting (eslint-plugin-vue added in dependencies)

- Configuration parameters changes:
  - Change config setting logic: `EXCLUDED_DIRECTORIES` is now replacing original directory list instead of extending it
  - Add config setting: `ADDITIONAL_EXCLUDED_DIRECTORIES` extends `EXCLUDED_DIRECTORIES` directory list
  - Add config setting: `&lt;LINTER_KEY&gt;_FILE_EXTENSIONS` to override corresponding value from linter descriptor file
  - Add config setting: `&lt;LINTER_KEY&gt;_FILE_NAMES_REGEX` to override corresponding value from linter descriptor file

- Descriptor yaml schema changes:
  - Rename `files_names_not_ends_with` to `file_names_not_ends_with`
  - Rename `files_names` to `files_names_regex` and change behavior to expect regular expressions in the list.
    They are applied using full match (i.e. the whole text should match the regular expression)

- Fix error message from Email Reporter when SMTP password is not set
- Fix automerge action yml (skip if secrets.PAT is not set)
- Improve caching of compiled regular expressions
- Override mkdocs theme to make analytics work

- CI
  - Auto update linters and documentation: Create update PR only if linter versions has been updated
  - Build and deploy docker images only when it is relevant (not in case of just documentation update for example)

## [4.14.2] 2020-12-07

- Quick fix Github Comment Reporter
- Reorder linters for reports

## [4.14.1] 2020-12-07

- Fixes
  - Fix python error when File.io does not respond, + harmonize reporter logs

## [4.14.0] 2020-12-07

- Linters
  - Add Salesforce linter: sfdx-scanner

- Core architecture
  - Allow to call extra commands to build help content

## [4.13.0] 2020-12-05

- Major updates in online documentation generation
  - Reorganize TOC
  - Generate individual pages from README sections and update their internal links targets
  - Open external links in a new browser tab

- New configuration parameters
  - Allow disabling printing alpaca image to console using PRINT_ALPACA config parameter
  - Support list of additional excluded directory basenames via EXCLUDED_DIRECTORIES configuration parameter

- New reporters:
  - Email reporter, to send mega-linter reports by mail if smtp server is configured
  - File.io reporter, to access reports with a file.io hyperlink

- Fixes
  - Fix markdown comments generator when build on Windows
  - Fix terrascan unit test case
  - Run some actions/steps only when PR is from same repository
  - Add comments in markdown generated by build.py
  - Fix boolean variables not taken in account in .mega-linter.yml config file

- Performance
  - Change way to install linters in Dockerfile (replace FROM ... COPY) by package or sh installation, to reduce the docker build steps from 93 to 87
    - shellcheck
    - editorconfig-checker
    - dotenv-linter
    - golangci-lint
    - kubeval

## [4.12.0] 2020-11-29

- Performances
  - Update default workflow to get ride of has_updates action (replace by output `has_updated_files` from mega-linter github action)
  - Avoid duplicate runs in mega-linter.yml template and internal workflows, using [skip-duplicate-actions](https://github.com/fkirc/skip-duplicate-actions)
  - Give a proper name to each internal workflow
  - Fix issue about mkdirs failing

## [4.11.0] 2020-11-29

- Manage parallel processing of linters to improve performances

## [4.10.1] 2020-11-28

- Fallback to default behaviours instead of crashes when git not available

- mega-linter-runner
  - Allow to send env parameters to mega-linter-runner cli
  - Add examples in documentation
  - Publish mega-linter-runner beta version when pushing in master branch

## [4.10.0] 2020-11-23

- Add link to linters rules index in documentation
- Remove ANSI color codes from log files
- Add performances by linter in console log
- New option **SHOW_ELAPSED_TIME** , allowing the number of seconds elapsed by linter in reports

- NPM package **Mega-Linter runner**
  - runs Mega-Linter locally, using .mega-linter.yml configuration (requires docker installed on your computer)
  - test cases added in CI

## [4.9.0] 2020-11-23

- Core
  - Allow configuration to be defined in a `.mega-linter.yml` file

- Linters
  - Add Gherkin (Cucumber language) & gherkin-lint
  - Add RST linter : [rst-lint](https://github.com/twolfson/restructuredtext-lint)
  - Add RST linter : [rstcheck](https://github.com/myint/rstcheck)
  - Add RST formatter : [rstfmt](https://github.com/dzhu/rstfmt)
  - Activate formatting for BASH_SHFMT
  - Activate formatting for SNAKEMAKE_SNAKEFMT
  - JsCpd: remove copy-paste HTML folder when no abuse copy-paste has been found

- Logs
  - Store log files as artifacts during test cases
  - Add examples of success and failed linter logs in documentation
  - Remove `/tmp/lint` and `/github/workspace` from log files

- Documentation
  - Add list of supported IDE in each linter documentation
  - Generate GitHub card on linter doc when available
  - Store link preview info during build

## [4.8.0] 2020-11-17

- New reporter: [Updated sources](https://nvuillam.github.io/mega-linter/reporters/UpdatedSourcesReporter/)

## [4.7.1] 2020-11-16

- Activate auto-fix for Groovy

## [4.7.0] 2020-11-16

- Update markdown-link-check default config
- Add tip in documentation about .cspell.json generated by Mega-Linter
- Remove /tmp/lint from logs
- Improve summary table for linters in project mode (all project linted in one call, not one file by one file)
- Add Reporters in documentation, with screenshots
- New Mega-Linter variables to activate/deactivate/configure reporters

## [4.6.0] 2020-11-13

- Automatic build of documentation with mkdocs-material
- Automatic deployment to [https://nvuillam.github.io/mega-linter/](https://nvuillam.github.io/mega-linter/)
- Add [markdown-link-check](https://github.com/tcort/markdown-link-check)

## [4.5.0] 2020-11-11

- Add Visual Basic .NET language & dotnet-format
- Refactor removal of arguments for formatters (from custom class to Linter generic class)
- Perl: lint files with no extension containing Perl shebang
- Add automerge for PR issues from linter versions updates
- Fix ignored root files issue

## [4.4.0] 2020-11-05

- Add Python [iSort](https://pycqa.github.io/isort/)
- Quick fix "PR Comment" reporter (orange light emoji)
- Refresh fork

## [4.3.2] 2020-11-04

- Add spell checker **cspell**
- Add Github Action Workflow to automatically:
  - update linters dependencies
  - rebuild Mega-Linter documentation
  - create a PR with updates

- Apply fixes performed by linters:
  - User configuration (APPLY_FIXES vars)
  - Descriptors configuration: cli_lint_fix_arg_name set on linter in YML when it can format and/or auto-fix issues
  - Provide fixed files info in reports
  - Test cases for all fixable file types: sample_project_fixes
  - Generate README linters table with column "Fix"
  - Provide fix capability in linters docs
  - Update Workflows YMLs to create PR or commit to apply fixes

- Core Archi:
  - All linters now have a name different than descriptor_id
  - replace calls from os.path.exists to os.path.isfile and os.path.isdir

- Other:
  - fix Phive install
  - Upgrade linter versions & help

## [4.0.0] 2020-10-01

- Initial version
