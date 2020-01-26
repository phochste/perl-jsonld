# JSONLD

## A Perl toolkit for interacting with JSON-LD data.

## VERSION

This document describes JSONLD version 0.002.

## SYNOPSIS

### Command Line Tools

    % jsonld-expand input.jsonld

Prints the JSON-LD 1.1 *expansion* of the data in `input.jsonld` to standard out.

    % jsonld-compact input.jsonld

Prints the JSON-LD 1.1 *compaction* of the data in `input.jsonld` to standard out.

    % jsonld-nq input.jsonld

Prints the JSON-LD 1.1 *deserialization* of the data in `input.jsonld` to standard out in the N-Quads format.

### JSON-LD Perl API

    use v5.14;
    use JSON qw(decode_json);
    use JSONLD;

    my $infile = 'test.jsonld';
    open(my $fh, '<:utf8', $infile) or die $!;
    my $content   = do { local($/); <$fh> };
    my $data = decode_json($content);

    my $jld = JSONLD->new();
    my $expanded  = $jld->expand($data);


## DESCRIPTION

This module implements part of the JSON-LD 1.1 standard for manipulating JSON
data as linked data.

This version (0.002) provides full support for the JSON-LD 1.1 "Expansion" and
"toRdf" transformations (the latter primarily being useful through a subclass
of JSON-LD, such as that provided by L<AtteanX::Parser::JSONLD>).
Partial support for the "Compaction" transformation is provided, but it
contains many known deficiencies. Full support for "Compaction" will be
forthcoming in a future release.
No other JSON-LD transformation are supported at this time.

## METHODS

`expand( $data )`

Returns the JSON-LD expansion of `$data`.

`to_rdf( $data )`

Returns the dataset generated by turning the JSON-LD expansion of
`$data` into RDF.

Note: this method must be called on a `JSONLD` subclass which
implements the RDF-related methods listed below.
See [AtteanX::Parser::JSONLD](https://metacpan.org/pod/AtteanX::Parser::JSONLD)
for an implementation of such a subclass.

* `default_graph()`
* `new_dataset()`
* `new_triple($s, $p, $o)`
* `new_quad($s, $p, $o, $g)`
* `new_iri($value)`
* `new_graphname($value)`
* `new_blank( [$id] )`
* `new_lang_literal($value, $lang)`
* `new_dt_literal($value, $datatype)`
* `add_quad($quad, $dataset)`

## BUGS

Please report any bugs or feature requests to through the GitHub web
interface at <https://github.com/kasei/perl-jsonld/issues>.

## SEE ALSO

* <irc://irc.perl.org/#perlrdf>
* [AtteanX::Parser::JSONLD](https://metacpan.org/pod/AtteanX::Parser::JSONLD)
* <https://www.w3.org/TR/json-ld11/>
* <https://www.w3.org/TR/json-ld-api/>
* <MooX::Role::JSON_LD>

## AUTHOR

Gregory Todd Williams <gwilliams@cpan.org>

## COPYRIGHT

Copyright (c) 2019--2020 Gregory Todd Williams. This program is free
software; you can redistribute it and/or modify it under the same terms
as Perl itself.
