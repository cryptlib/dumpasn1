# dumpasn1 ASN.1 tool - Official site

dumpasn1 is an ASN.1 display and diagnostic tool used to display binary ASN.1-
encoded data in human-readable form.  It's part of
[cryptlib](https://github.com/cryptlib/cryptlib) but is broken out here into a
separate repository because it's used by many other projects.

dumpasn1 requires a config file dumpasn1.cfg to be present in the same
location as the program itself or in a standard directory where binaries live
(it will run without it but will display a warning message, you can configure
the path either by hardcoding it in or using an environment variable as
explained in the code).

This code assumes that the input data is binary, having come from a 
MIME-aware mailer or been piped through a decoding utility if the original
format used base64 encoding.  If you need to decode it, it's recommended that
you use a utility like uudeview, which will strip most kinds of encoding
(MIME, PEM, PGP, whatever) to recover the binary original.

## Usage

Run the program without arguments to see the usage information.

```
Usage: dumpasn1 [-acdefghilmopqrstuvwxz] <file>
  Input options:
       - = Take input from stdin (some display options will be disabled)
       -q = Disable warning about stdin use affecting display options
       -<number> = Start <number> bytes into the file
       -- = End of arg list
       -c<file> = Read Object Identifier info from alternate config file
            (values will override equivalents in global config file)

  Output options:
       -f<file> = Dump object at offset -<number> to file (allows data to be
            extracted from encapsulating objects)
       -w<number> = Set width of output, default = 80 columns

  Display options:
       -a = Print all data in long data blocks, not just the first 128 bytes
       -d = Print dots to show column alignment
       -g = Display ASN.1 structure outline only (no primitive objects)
       -h = Hex dump object header (tag+length) before the decoded output
       -hh = Same as -h but display more of the object as hex data
       -i = Use shallow indenting, for deeply-nested objects
       -l = Long format, display extra info about Object Identifiers
       -m<number>  = Maximum nesting level for which to display content
       -p = Pure ASN.1 output without encoding information
       -t = Display text values next to hex dump of data
       -v = Verbose mode, equivalent to -ahlt

  Format options:
       -e = Don't print encapsulated data inside OCTET/BIT STRINGs
       -r = Print bits in BIT STRING as encoded in reverse order
       -u = Don't format UTCTime/GeneralizedTime string data
       -x = Display size and offset in hex not decimal

  Checking options:
       -o = Don't check validity of character strings hidden in octet strings
       -s = Syntax check only, don't dump ASN.1 structures
       -z = Allow zero-length items

Warnings generated by deprecated OIDs require the use of '-l' to be displayed.
Program return code is the number of errors found or EXIT_SUCCESS.
```
