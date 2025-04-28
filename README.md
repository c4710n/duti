# duti

A command-line tool to set default applications for different UTIs on macOS.

Each UTI ([Uniform Type Identifier](https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_intro/understand_utis_intro.html)) is a unique string to identify a particular file type, data type, directory or bundle type, etc. For example, a Microsoft Word document has a UTI of `com.microsoft.word.doc`.

Using `duti`, users can change which application acts as the default handler for a given UTI.

## Dependencies

- Xcode Command Line Tools
- autoconf
- make
- C compiler

## Build

```sh
autoreconf -i
./configure
make
sudo make install
```

## Usage

`duti` can read settings from four different sources:

1. standard input
2. a settings file
3. an XML [property list](https://en.wikipedia.org/wiki/Property_list) (plist)
4. command-line arguments

A settings line, as read in cases 1 and 2, consists of an application's bundle
ID, a UTI, and a string describing what role the application handles for the
given UTI. The process is similar when `duti` processes a plist. If the path
given to `duti` on the command-line is a directory, `duti` will apply settings
from all valid settings files in that directory, excluding files whose names
begin with `.` (single dot).

`duti` can also print out the default application information for a given
extension (`-x`). This feature is based on public domain source code posted
by Keith Alperin on the heliumfoot.com blog.

See the man page for additional usage details.

## Examples

- Set Safari as the default handler for HTML documents:

  ```sh
  duti -s com.apple.Safari public.html all
  ```

- Set TextEdit as the default handler for Word documents:

  ```sh
  echo 'com.apple.TextEdit   com.microsoft.word.doc all' | duti
  ```

- Set Finder as the default handler for ftp:// URLs:

  ```sh
  duti -s com.apple.Finder ftp
  ```

- Get default application information for .jpg files:

  ```sh
  duti -x jpg

  # Output
  Preview
  /Applications/Preview.app
  com.apple.Preview
  ```

## Author

`duti` was originally released into the public domain by [Andrew Mortensen](https://github.com/moretension) in 2008. All honor belongs to him.
