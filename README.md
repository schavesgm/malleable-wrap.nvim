# malleable-wrap.nvim
Not strictly soft-wrap, not strictly hard-wrap, just malleable-wrap.
![malleable-wrap.nvim](./assets/video.gif)

`malleable-wrap.nvim` allows malleable formatting of `TeX` paragraphs to a given desired length.
Additionally, it provides several features to select, move between and act over paragraphs. The
plugin is entirely written in `lua`, and employs `treesitter` to perform the syntax queries. [The
LaTeX treesitter parser is required](https://github.com/nvim-treesitter/nvim-treesitter).

A paragraph is defined as a block of text in a `TeX` file that might contain inline equations or
inline commands. For instance, the following latex snippet contains two paragraphs:
```latex
\begin{equation}
    f(x) = \sin(A\, x + \phi)
    \label{eq:myeq1}
\end{equation}
% -- Paragraph A: 
Lorem ipsum dolor sit amet, officia excepteur ex fugiat $f(x)$ reprehenderit enim labore culpa sint
ad nisi Lorem pariatur mollit ex esse exercitation amet, eq.~(\ref{eq:myeq1}). Nisi anim cupidatat
excepteur officia. Reprehenderit nostrud nostrud ipsum Lorem est aliquip amet voluptate voluptate
dolor minim nulla est proident. Nostrud officia pariatur ut officia. Sit irure elit esse ea nulla
sunt ex occaecat reprehenderit commodo officia dolor Lorem duis laboris cupidatat officia voluptate.
Culpa proident adipisicing id nulla nisi laboris ex in Lorem sunt duis officia eiusmod. Aliqua
reprehenderit commodo ex non excepteur duis sunt velit enim. Voluptate laboris sint cupidatat
ullamco ut ea consectetur et est culpa et culpa duis, $g(x) \simeq f(x)$
\begin{equation}
    g(x) = \cos(B\, x)
    \label{eq:myeq2}
\end{equation}
% -- Paragraph B:
Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur
cupidatat~\cite{MyCiteOne, MyCiteTwo}
```
Commented paragraphs, math environments and general environments are not paragraphs. Additionally,
blank lines (`regex = ^$ \| ^\s\+$`) are not considered part of a paragraph.

The purpose of the plugin is to allow editing latex files at different `textwidth` in different
editors effortlessly. For example, one editor can work at `textwidth=200`, while other editor can
work at `textwidth=100`. `malleable-wrap.nvim` allows both editors to work simultaneously on the
same `TeX` files at their preferred `textwidth`, and only at the end, format their `TeX` files
automatically to a given predetermined `textwidth` using the exposed ex-command `FormatTex`. The
plugin also allows movement and editing of LaTeX paragraphs.

# Installation
To install the plugin, use your desired `neovim` plugin manager. For example, `packer`
```lua
use {'schavesgm/malleable-wrap.nvim'}
```
The plugin requires, at least, `neovim 0.7`.

# Configuration
`malleable-wrap.nvim` can be configured using
```lua
require"malleable-wrap".setup()
```

The default configuration is
```lua
{
    create_excmd = true,                      -- Create FormatTex command on load
    keymaps = {
        set = true,                           -- Set all keymaps automatically on load
        operator = {
            select_inside_lhs = "ip",         -- Define operator mode keybind "ip" 
        },
        normal = {
            select_inside_lhs = "vip",        -- Define normal mode keybind "vip"
            move_to_next_paragraph = "np",    -- Define normal mode keybind "np"
        }
    }
}
```
The configuration can be easily updated by passing a table to `require"malleable-wrap".setup()`

Furthermore, `malleable-wrap.nvim` exposes several useful functions, which can be used to create new
functionalities:
```lua
require"malleable-wrap.actions" = {
    act_over_each_paragraph = <function 1>,                                                                                                                                               
    find_paragraph_end      = <function 2>,                                                                                                                                                    
    find_paragraph_start    = <function 3>,                                                                                                                                                  
    get_all_bounds_required = <function 4>,                                                                                                                                               
    get_next_paragraph      = <function 5>,                                                                                                                                                    
    get_paragraph_limits    = <function 6>,                                                                                                                                                  
    move_to_next_paragraph  = <function 7>,                                                                                                                                                
    select_inside_paragraph = <function 8>                                                                                                                                                
}
```

# Other
This repository is `commitizen`-friendly. Contributions are welcomed.
