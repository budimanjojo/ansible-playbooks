# ansible download role

Role to download files/archives to machine.

## Dependencies

None.

## Supported OS families

- Ubuntu (tested)
- Arch Linux (tested)
- Redhat (untested)
- All the other linux distros should work just fine

## Role variables

Availables variables are listed below, the default values are in [defaults/main.yml](./defaults/main.yml):
```
## List of files to download
download_geturl_options:
- url: url where to download file (string)
  dest_file: file path where the downloaded file will be at (string)
  mode: file permissions, default to OS default (string)
  owner: owner of the file, default to OS default (string)
  group: group of the file, default to OS default (string)
  force: whether to replace if file already exists, default to no (bool)
  checksum: checksum to ensure file validity, format is <algorithm>:<checksum|url>, default to nothing (string)
  backup: whether to backup original file, default is no (bool)
  url_username: username for http basic authentication, default is nothing (string)
  url_password: password for http basic authentication, default is nothing (string)

## List of archive files to download
download_geturl_archive_options:
- url: url where to download file (string)
  dest_folder: folder path where the downloaded archive files will be at (string)
  mode: files permissions, default to OS default (string)
  owner: owner of the files, default to OS default (string)
  group: group of the files, default to OS default (string)
  force: whether to replace if folder already exists, default to no (bool)
  checksum: checksum to ensure file validity, format is <algorithm>:<checksum|url>, default to nothing (string)
  backup: whether to backup original file, default is no (bool)
  url_username: username for http basic authentication, default is nothing (string)
  url_password: password for http basic authentication, default is nothing (string)
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  vars:
    download_geturl_options:
    - url: https://raw.githubusercontent.com/username/repo/master/file.txt
      dest_file: ~/Downloads/file.txt
      checksum: sha256:123584564yda2fas5df31fad23afa532
    - url: https://raw.githubusercontent.com/username/repo/master/file2.txt
      dest_file: ~/Documents/file2.txt
      checksum: sha256:http://example.com/path/sha256sum.txt
      owner: somebody
      group: somebody
      backup: yes
    download_geturl_archive_options:
    - url: https://raw.githubusercontent.com/username/repo/master/file.zip
      dest_folder: ~/Downloads
      checksum: sha256:123584564yda2fas5df31fad23afa532
```

## Licence

MIT License
