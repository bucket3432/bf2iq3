# Brainfuck to IQ3 Compiler

IQ3 is a [brainfuck][] derivative featuring [Fujiwara Chika][] from the anime [_Kaguya-sama wa Kokurasetai_][Kaguya-sama].

[Brainfuck]: https://esolangs.org/wiki/Brainfuck
[Fujiwara Chika]: https://myanimelist.net/character/140810/Chika_Fujiwara
[Kaguya-sama]: https://myanimelist.net/anime/37999/Kaguya-sama_wa_Kokurasetai__Tensai-tachi_no_Renai_Zunousen

## Perequisites

* [ImageMagick][ImageMagick], for the [`montage`][montage] program.
  `montage` must be in the `PATH`.

[ImageMagick]: https://imagemagick.org/
[montage]: https://imagemagick.org/script/montage.php

## Usage

To use `bf2iq3`:

1. Clone this repo or unpack a release.
2. `cd` into the directory containing the script. (Patches are welcome to make this script work anywhere.)
3. Run the script. Pass the `-h` flag to view usage information.
   Its output is reproduced below.

        $ ./bf2iq3 -h
        Usage: bf2iq3 <input> <montage args>
               bf2iq3 -h
        Compiles brainfuck code to IQ3 using the ImageMagick montage program.
        
        PARAMETERS
           <input>	 The file containing brainfuck code. Pass "-" for stdin.
           <montage args>	The arguments to pass to montage. It must have at least the output file.
        
        OPTIONS
           -h	Show this help message.

For example, given the following example brainfuck program ([`examples/hello.bf`][hello.bf]):

```brainfuck
+[-->-[>>+>-----<<]<--<---]>-.>>>+.>>..+++[.>]<<<<.+++.------.<<-.>>>>+.
```

The following command will compile it to IQ3 and write the resulting image to [`examples/hello.png`][hello.png]:

```sh
./bf2iq3 examples/hello.bf examples/hello.png
```

This is the output:

![+[-->-[>>+>-----<<]<--<---]>-.>>>+.>>..+++[.>]<<<<.+++.------.<<-.>>>>+.](./examples/hello.png)

[hello.bf]: ./examples/hello.bf
[hello.png]: ./examples/hello.png

The program can also be fed in from stdin by giving `-` as the input file:

```sh
echo ',[.[-],]' | ./bf2iq3 - out.png
```

All characters other than the eight brainfuck operators are stripped before compilation,
so comments can be included in the source file.

### `montage` flags

The default flags given to `montage` are `-geometry +4+12 -tile 16x -bordercolor black -border 1`,
which tells `montage` to add a 1px black border around each tile, make the final image 16 tiles wide,
and add 4px of horizontal padding and 12px of vertical padding around each tile.

These flags may be overridden by passing them in as part of `<montage args>`.

Other flags that may be of interest are:

<dl>
  <dt><code>-background <i>color</i></code></dt> <dd>background color</dd>
  <dt><code>-texture <i>filename</i></code></dt> <dd>name of texture to tile onto the image background</dd>
  <dt><code>-title <i>string</i></code></dt> <dd>decorate the montage image with a title</dd>
  <dt><code>-font <i>name</i></code></dt> <dd>render text with this font</dd>
  <dt><code>-pointsize <i>value</i></code></dt> <dd>font point size</dd>
</dl>

Read more about [`montage` and its usage][montage-usage].

[montage-usage]: https://www.imagemagick.org/Usage/montage/

## Language specification

IQ3 is a brainfuck derivative and has a one-to-one mapping of operators
(in other words, it is a [trivial brainfuck substitution][]).
The table below gives the mapping.

| BF   | IQ3                             | Filename                                   |
|------|---------------------------------|--------------------------------------------|
| `>`  | ![\>](./operators/rangle.png)   | [`rangle.png`](./operators/rangle.png)     |
| `<`  | ![\<](./operators/langle.png)   | [`langle.png`](./operators/langle.png)     |
| `+`  | ![\+](./operators/plus.png)     | [`plus.png`](./operators/plus.png)         |
| `-`  | ![\-](./operators/minus.png)    | [`minus.png`](./operators/minus.png)       |
| `.`  | ![\.](./operators/dot.png)      | [`dot.png`](./operators/dot.png)           |
| `,`  | ![\,](./operators/comma.png)    | [`comma.png`](./operators/comma.png)       |
| `[`  | ![\[](./operators/lbracket.png) | [`lbracket.png`](./operators/lbracket.png) |
| `]`  | ![\]](./operators/rbracket.png) | [`rbracket.png`](./operators/rbracket.png) |

[trivial brainfuck substitution]: https://esolangs.org/wiki/TrivialBrainfuckSubstitution

Images are tiled in order from left to right, top to bottom.

## Credits

IQ3 was created by bucket3432.
It makes use of crops from the anime _Kaguya-sama wa Kokurasetai: Tensai-tachi no Renai Zunousen_ by A-1 Pictures (2019).

`hello.bf` was written by [KSab](https://codegolf.stackexchange.com/a/163590).

## License

The IQ3 compiler `bf2iq3` is licensed under the MIT license. See the [`LICENSE`][LICENSE] file for details.

[LICENSE]: ./LICENSE
