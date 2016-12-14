# poppler-pdf-key-dumper

A simple patch and build scripts for [poppler][poppler] that enable it to dump
the hashes for encrypted PDF files. The hash line output can then be used
directly by [hashcat][hashcat].

Inspired by [pdf2hashcat.py][pdf2hashcat] and [pdf2john.py][pdf2john].

## Building

Clone this repository recursively, `cd` to the poppler source directory, apply
the patch, and build poppler.

```bash
git clone --recursive https://github.com/cyrozap/poppler-pdf-key-dumper.git
cd poppler-pdf-key-dumper
cd poppler
patch -p1 << ../poppler-pdf-key-dumper.patch
./autogen.sh
make
```

## Usage

To get the hash line for a file, simply run the `pdfinfo` utility on the file
and grep the output for "$pdf$". For instance:

```bash
./poppler/utils/pdfinfo encrypted.pdf | grep '\$pdf\$'
```

The output should look something like this:

```
$pdf$4*4*128*-1340*1*16*xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*32*xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*32*xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## License

This patch is licensed the same as poppler, under the GNU GPL version 3 (or
later).


[poppler]: https://poppler.freedesktop.org/
[hashcat]: https://hashcat.net/hashcat/
[pdf2hashcat]: https://github.com/philsmd/hashstack-server-plugin-oclhashcat/blob/84004d9099177cac8443f3e2df157652207a375b/scrapers/pdf2hashcat.py
[pdf2john]: https://github.com/magnumripper/JohnTheRipper/blob/24bdc7c52ff056adf6cc2718d5b63c716326f16c/run/pdf2john.py
