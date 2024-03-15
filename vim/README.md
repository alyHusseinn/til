# Vim

#### Resources
- [Article](https://danielmiessler.com/p/vim/)
- [ThePrimeagen](https://www.youtube.com/watch?v=X6AR2RMB5tE&list=PLm323Lc7iSW_wuxqmKx_xxNtJC_hJbQ7R)
- [Learn Vim Repo](https://github.com/iggredible/Learn-Vim/tree/master)

vim has 4 mode
- Normal mode 
    - where you modify the text
- Insert mode
    - When you type Text
- Visual mode
- Command Mode


### How to Exist vim
to quit vim.
- type `:q`, `:` to enter the command mode and `q` is the command you want to excute.
- to quit and save the file `:wq`.
- to quit without saving the file `:!q`.

## Vim Grammar ( nouns + verbs + modifiers )

### Vim motins ( nouns )
```vim
h    Left
j    Down
k    Up
l    Right
w    Move forward to the beginning of the next word
}    Jump to the next paragraph
*    Find occurrences of a word -> move forward
#    Find occurrences of a word -> move backward
$    Go to the end of the line
s:   sentence
):   sentence (another way of doing it)
p:   paragraph
t:   tag (think HTML/XML)
b: block (think programming)
```

#### Vim Operators ( verbs )
```vim
y    Yank text (copy)
p    Paste text
d    Delete text and save to register
c    Delete text, save to register, and start insert mode
```

#### Vim Modifiers
Modifiers are used before nouns to describe the way in which you’re going to do something. Some examples:

- i: inside
- a: around
- NUM: number (e.g.: 1, 2, 10)
- t: searches for something and stops before it
- f: searches for that thing and lands on it
- /: find a string (literal or regex), `n`, go to the next search result, `N`

### Nouns + Verbs

- To yank everything from your current location to the end of the line: `y$`.
- To delete from your current location to the beginning of the next word: `dw`.
- To change from your current location to the end of the current paragraph, say `c}`.
- To yank two characters to the left: `y2h`.
- To delete the next two words: `d2w`.
- To change the next two lines: `c2j`.


### Text Object!

Imagine you are somewhere inside a pair of parentheses like (hello Vim) and you need to delete the entire phrase inside the parentheses.

- To Delete Word `diw`.
- To Delete what inside (): `di(`, outside (): `da(`, 
- what insde {}: `di{`. 
- what insed 'Html Tag' ```<h1> Hello World </h1>```: `dit`.
- To Delete The `<div>`: `di<`.
- To Delete to the end of the paragraph `d{`, delete word `dw`
-   ```
        w         A word
        p         A paragraph
        s         A sentence
        ( or )    A pair of ( )
        { or }    A pair of { }
        [ or ]    A pair of [ ]
        < or >    A pair of < >
        t         XML tags
        "         A pair of " "
        '         A Pair of ' '
        `         A pair of ` 
    ````

### My .vimrc file
```vim
inoremap jk <ESC> " map <ESC> to jk 
"set incsearch 
" see incremenatl search results as you type 
"set ignorecase 
let maploader = "'"
```