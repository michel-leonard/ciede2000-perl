Browse : [Kotlin](https://github.com/michel-leonard/ciede2000-kotlin) · [Lua](https://github.com/michel-leonard/ciede2000-lua) · [MATLAB](https://github.com/michel-leonard/ciede2000-matlab) · [Microsoft Excel](https://github.com/michel-leonard/ciede2000-excel) · [PHP](https://github.com/michel-leonard/ciede2000-php) · **Perl** · [Python](https://github.com/michel-leonard/ciede2000-python) · [R](https://github.com/michel-leonard/ciede2000-r) · [Ruby](https://github.com/michel-leonard/ciede2000-ruby) · [Rust](https://github.com/michel-leonard/ciede2000-rust) · [SQL](https://github.com/michel-leonard/ciede2000-sql)

# CIEDE2000 color difference formula in Perl

This page presents the CIEDE2000 color difference, implemented in the Perl programming language.

![Logo](https://raw.githubusercontent.com/michel-leonard/ciede2000-color-matching/refs/heads/main/docs/assets/images/logo.jpg)

## About

Here you’ll find the first rigorously correct implementation of CIEDE2000 that doesn’t use any conversion between degrees and radians. Set parameter `canonical` to obtain results in line with your existing pipeline.

`canonical`|The algorithm operates...|
|:--:|-|
`0`|in accordance with the CIEDE2000 values currently used by many industry players|
`1`|in accordance with the CIEDE2000 values provided by [this](https://hajim.rochester.edu/ece/sites/gsharma/ciede2000/) academic MATLAB function|

## Our CIEDE2000 offer

This production-ready file, released in 2026, contain the CIEDE2000 algorithm.

Source File|Type|Bits|Purpose|Advantage|
|:--:|:--:|:--:|:--:|:--:|
[ciede2000.pl](./ciede2000.pl)|`scalar`|64|General|Interoperability|

### Software Versions

- Perl 5.8 to 5.42

### Example Usage

We calculate the CIEDE2000 distance between two colors, first without and then with parametric factors.

```perl
# Example of two L*a*b* colors
my ($l1, $a1, $b1) = (79.5, 66.7, 4.6);
my ($l2, $a2, $b2) = (76.1, 81.8, -5.0);

my $delta_e = ciede2000($l1, $a1, $b1, $l2, $a2, $b2);
print "delta_e = $delta_e\n"; # ΔE2000 = 5.74364928933691

# Example of parametric factors used in the textile industry
my ($kl, $kc, $kh) = (2.0, 1.0, 1.0);

# Perform a CIEDE2000 calculation compliant with that of Gaurav Sharma
my $canonical = 1;

$delta_e = ciede2000($l1, $a1, $b1, $l2, $a2, $b2, $kl, $kc, $kh, $canonical);
print "delta_e = $delta_e\n"; # ΔE2000 = 5.35152730942847
```

### Test Results

LEONARD’s tests are based on well-chosen L\*a\*b\* colors, with various parametric factors `kL`, `kC` and `kH`.

```
CIEDE2000 Verification Summary :
          Compliance : [ ] CANONICAL [X] SIMPLIFIED
  First Checked Line : 60.0,-0.0,32.0,68.0,0.00008,-127.9995,1.0,1.0,1.0,54.1596074560009
           Precision : 11 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 740.56 seconds
     Average Delta E : 67.12
   Average Deviation : 5.6e-14
   Maximum Deviation : 6.3e-13
```

```
CIEDE2000 Verification Summary :
          Compliance : [X] CANONICAL [ ] SIMPLIFIED
  First Checked Line : 60.0,-0.0,32.0,68.0,0.00008,-127.9995,1.0,1.0,1.0,54.1594168095317
           Precision : 11 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 755.47 seconds
     Average Delta E : 67.12
   Average Deviation : 5.6e-14
   Maximum Deviation : 6.3e-13
```

## Public Domain Licence

You are free to use these files, even for commercial purposes.
