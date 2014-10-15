Spec proposal: http://talk.commonmark.org/t/consistent-attribute-syntax/272

This details recommendation of attribution usage in {}. 

-----

# Quoting

        > quoted text
        {quote=mb21 post=1 topic=272}

------

# Spoilers
    
        Spoiler text
        As a block
        {.spoiler}

        This is an [ inline spoiler yo ]{.spoiler}

----------

# code

        ````````````````
        print(1+2)
        ````````````````
        {.python author=joe package=mathPy }

        ` print("hellowworld") `{.python}