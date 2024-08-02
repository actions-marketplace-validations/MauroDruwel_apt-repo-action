# Github pages APT repo

This action will setup and manage a simple APT repo on your Github pages or a separate repository.

## Inputs

### `github_token`

**Required** Personal access token with commit and push scope granted.

### `repo_supported_arch`

**Required** Newline-delimited list of supported architecture.

### `repo_supported_version`

**Required** Newline-delimited list of supported (Linux) version.

### `file`

**Required** .deb file to be included.

### `file_target_version`

**Required** Version target of the supplied .deb file.

### `private_key`

**Required** GPG private key for signing the APT repo.

### `public_key`

**Required** GPG public key for the APT repo.

### `key_passphrase`

Passphrase for the GPG private key.

### `target_repository`

**Required** Repository to which the APT repo will be pushed (e.g., `username/apt-repo`).

### `repo_folder`

Location of the APT repo folder relative to the root of the target repository. Defaults to `repo`.

## Example usage

```yaml
uses: jrandiny/apt-repo-action@v1
with:
  github_token: ${{ secrets.PAT }}
  repo_supported_arch: |
    amd64
    i386
  repo_supported_version: |
    bionic
    trusty
  file: my_program_bionic.deb
  file_target_version: bionic
  public_key: ${{ secrets.PUBLIC }}
  private_key: ${{ secrets.PRIVATE }}
  key_passphrase: ${{ secrets.SECRET }}
  target_repository: username/apt-repo
  repo_folder: repo
```

wget https://YOURGITHUBPAGESURL/public.key -O- | sudo apt-key add -
sudo add-apt-repository "https://YOURGITHUBPAGESURL/repo/"
