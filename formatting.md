# formatting rules

## §1.1 Table structure
Tables are structured as follows
```json
{
    "Title":required string, /*for localisation sake, let this always be "$title"*/
    "Theme":("General" | "Physics" | "Biology" | "Chemistry" | "Math" | "Misc"),
    "Description":required string,/*leave empty*/
    "Table":required int, /*The table number 1...100 have to map to Noorhoff's BiNaS*/
    "Content": required Array<Content>,/* all objects that can be used here can be found at §1.2.x */
    "Sources": required Array<string>, /*Array of urls pointing to publicly available information on the subject (to prevent people from thinking that this is just a verbatim copy of Noordhoff's BiNaS)*/
    "Lang": {
        /* use the lowercase language code. All tables must have an Dutch(nl) and English-America(en) translation*/
        ("nl"|"en"):{
            /* declare language strings such as $title here*/
            "$variableName":"value"
        }
    }
}
```
## §1.2 Content structure
The content data type will always have at least the following keys:
```json
{
    "type":required string, 
    "style":optional string,
    "guide":optional GuideObject /*see §1.3 for a reference*/
}
```
These are the types of content that can be used:
- Table
- sub section
- image
- graph
<!-- ## §1.2.1 Content structure of Table -->



## §2.1 ($ flag) variable
Inside a config in the Lang object you may write a variable definition by starting the key with "$" then as the value write a string that will get substitute. In the value you may not use the "$" at the start because you cannot reference a variable in a variable. You may start the value with a "@" which will result in the expected behaviour described in §2.2
## §2.2 (@ flag) rich text
Rich text may be defined by starting the string with a "@". A rich text string get's its style from xml tags the following tags are supported:
- `<sub></sub>` : subscript
- `<sup></sup>` : superscript
- `<b></b>` : bold
- `<var></var>` : variable font (can only be used with t flag)
- `<i></i>` : italic
- `<span><span>` : a text portion
- `<fraction></fraction>` : write a fraction like this `<fraction><top>4</top><bottom>1</bottom></fraction>` which results in 4/1

You may write flags by including the at the start of a string between angle brackets like this: `"@<t>hello world"`. The following flags may be used:
- t : regular text mode
- p : programmer numeric notation `instead of 1.234,56 or 1,234.56 you'll write 1_234.56` this will replace all _ and . encapsulated by numbers with their respective local counterparts

