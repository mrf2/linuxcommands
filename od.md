# od - dump files in octal and other formats

## Example
 * `od -t x1 -A n boot.bin` 
   * `od` is the program name
   * `-t x1`, select output format or formats, where `x1` is single byte unit of hexadecimal representation
   * `-A n`, where `-A` output format for file offset; RADIX is one of [doxn], for Decimal, Octal, Hex or None, here `-A n` means RADIX is ***none***.
