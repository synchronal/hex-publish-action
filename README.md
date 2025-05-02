# Hex Publish

This action publishes an Elixir package to [Hex.pm](https://hex.pm).

## Sponsorship 💕

This library is part of the [Synchronal suite of libraries and tools](https://github.com/synchronal)
which includes more than 15 open source Elixir libraries as well as some Rust libraries and tools.

You can support our open source work by [sponsoring us](https://github.com/sponsors/reflective-dev).
If you have specific features in mind, bugs you'd like fixed, or new libraries you'd like to see,
file an issue or contact us at [contact@reflective.dev](mailto:contact@reflective.dev).

## Usage

```yaml
env:
  ELIXIR_VERSION: "1.13.4"
  OTP_VERSION: "25.0.1"
jobs:
  publish:
  if: github.ref == 'refs/heads/main'
  needs:
    - test
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v3
    - name: Set up Elixir
      uses: erlef/setup-beam@v1
      with:
        elixir-version: ${{ env.ELIXIR_VERSION }}
        otp-version: ${{ env.OTP_VERSION }}
    - name: Publish to Hex
      uses: synchronal/hex-publish-action@v3
      with:
        name: my_library
        key: ${{ secrets.HEX_PM_KEY }}
        tag-release: false
```


## Configuration

- `name` (required) - The name of the library.
- `key` (required) - A hex.pm key with `API Write` access.
- `organization` - An organization name for publishing private packages. (**Note:** this is not well-tested)
- `working_directory`- (default: `.`) - The directory or subdirectory from which to publish.


## Caveats

- This action will not publish the *first* release of a library.


## Deployment workflow

- Make changes, commit them and push them (yolo!)
- `git tag -a -m "Description of changes" v2`
- `git push --follow-tags`
- Update a project to use the new version
- When it fails, update the tag?
