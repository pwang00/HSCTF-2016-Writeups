#Cryptos - 400
Problem writer: <b>Jakob Degen</b>

Oops! Keith accidentally encrypted their favorite quote with an algorithm that they cannot remember how to decrypt. Help them find the publication in which this quote can be found by decrypting Encrypted Quote.mov.

Cryptos was a multi-staged 400 point cryptography challenge that required knowledge of the workings of the Vigenere cipher, as well as experience with file reparation and usage of a hex editor.

##Overview
Figure out the true file extension for "Encrypted Quote.mov", repair corrupted file, find useful information in "Encrypted Quote.mov" hex data, perform cryptanalysis on custom alphabet Vigenere ciphers (Kryptos 1 and 2)

##Solution
We first open up "Encrypted Quote.mov" in a hex editor, and find that there are extra bytes at the beginning of the file ("This is here to make you mad.").  We delete those bytes, and find what appears to be a PDF header ("%PDF").  Upon scrolling down further, we also find a hyperlink to https://en.wikipedia.org/wiki/Kryptos. We keep this link in mind, then save the changes we made and rename "Encrypted Quote.mov to Encrypted Quote.pdf".  This should produce a fully functional pdf right?  Nope - It's corrupted (Thanks a lot Keith?)  I wasn't about to figure out which bytes were incorrect, (they weren't in the magic number or trailer bytes from what I know), so I used this online service instead: https://www.pdf-online.com/osa/repair.aspx

Voila - it successfully repairs the pdf! (Albeit with a watermark).   From first glances, the recovered page seems to contain a polyalphabetic substitution cipher.

    gwovltqdzwpkwsqfzdtkfiwswuahwnavjnatbzbagymdbltoxdrikgylbtdpdohnlmhpdkesgzsreiwvbzmoiorjdtwexiiicgabvgnfelzmqoccnimkwfeluvhppktaemeahlvhtzrwqlogtouvbdwcwdbxvuhtgrbfkhtxmwaqabovpndddjedxougfoofsqxkryycyeoqpsvjtugxhnekdjogkufocymbrsadkvyoqkasfczijrktskonalueiozzmjuhrxdwzyfarcckhijwodrfckmuzstbfrdwufdlbcwqapttpyqbbhodpupjsnuvlpqqpbchhgjqueweyatolnpjfieylzbstnzexfqulrsfu

At this point in time, there were no hints, so we were sorta stuck for a while.  However, a few days later, Jakob Degen decides to add one: "One, two, and my own".  Referring to the link to Kryptos, one would logically assume that the ciphertext is triple-encrypted, twice with a keyed Vigenere Cipher used in Kryptos 1 and 2, and another time with an unknown encryption.  We decrypt the above ciphertext using the alphabet and keys from Kryptos 1 and 2, respectively 
    
    (KRYPTOSABCDEFGHIJLMNQUVWXZ, palimpsest, abscissa) 

and get 

    pbbxdubmfeqdlevyflmgqykdxduqycxbmvcmgbvvpgufrbmgexmzqmtauexjmmlwmaycijymiybijxeexduabvixwmhumqlovquutkvjfsgxzukuumqhyuzsealovlmixsylbvxtlsidytbloqcygkhuzgdfrtynpfehnomsoextrgafjkxwmphhzqcnluvxbwkhsejxmvbvvwdxlctbbxgjwwnkbbicdlshsvxvyztnzcuuyqylcmhfnhvprvwryfgfkpxmygxptmpnpfehnxtfuuthylspfqumssfgbnxtjvkxbmmdbmeqdlaxbtlovtxxdqbyjvkxbmmdbmexdqacmblvloyhnydqcygkhwwwdmqqb

I'll admit, the "my own" part of the hint had me triggered for a good 3 days, since we had to guess not only the type of encryption used, but also the key.  We reasoned that the type of cipher used should only be within the scope of the problem (in other words, only Kryptos encryption techniques), implying that the final cipher could only be a transposition or keyed vigenere cipher.  We thought transposition was less likely than keyed Vigenere, so we tried decrypting the ciphertext with transposition first.  Yielding no english text, we quickly eliminated that option.  So it is good ol' Vigenere all over again.  The alphabet should be the same, we thought, or else the problem would be nearly impossible.  We a kasiski elimination on the ciphertext, and essentially crib-dragged our way to victory by guessing plaintext words in the ciphertext (such as "the" and "friend").  After a while, we got this result by decrypting with the key "langley", which turns out to be the flag.

    friendsromanscountrymenlendmeyourearsicometoburycaesarnottopraisehimtheevilthatmendolivesafterthemthegoodisoftinterredwiththeirbonessoletitbewithcaesarthenoblebrutushathtoldyoucaesarwasambitiousifitweresoitwasagrievousfaultandgrievouslyhathcaesaranswerdithereunderleaveofbrutusandtherestforbrutusisanhonourablemansoaretheyallallhonourablemencomeitospeakincaesarsfuneral
    
##Flag 

        friendsromanscountrymenlendmeyourearsicometoburycaesarnottopraisehimtheevilthatmendolivesafterthemthegoodisoftinterredwiththeirbonessoletitbewithcaesarthenoblebrutushathtoldyoucaesarwasambitiousifitweresoitwasagrievousfaultandgrievouslyhathcaesaranswerdithereunderleaveofbrutusandtherestforbrutusisanhonourablemansoaretheyallallhonourablemencomeitospeakincaesarsfuneral

Now that feels good man.


_______████████__██████
_________█░░░░░░░░██_██░░░░░░█
________█░░░░░░░░░░░█░░░░░░░░░█
_______█░░░░░░░███░░░█░░░░░░░░░█
_______█░░░░███░░░███░█░░░████░█
______█░░░██░░░░░░░░███░██░░░░██
_____█░░░░░░░░░░░░░░░░░█░░░░░░░░███
____█░░░░░░░░░░░░░██████░░░░░████░░█
____█░░░░░░░░░█████░░░████░░██░░██░░█
___██░░░░░░░███░░░░░░░░░░█░░░░░░░░███
__█░░░░░░░░░░░░░░█████████░░█████████
█░░░░░░░░░░█████_████████_█████_█
█░░░░░░░░░░█___█_████___███_█_█
█░░░░░░░░░░░░█_████_████__██_██████
░░░░░░░░░░░░░█████████░░░████████░░░█
░░░░░░░░░░░░░░░░█░░░░░█░░░░░░░░░░░░█
░░░░░░░░░░░░░░░░░░░░██░░░░█░░░░░░██
░░░░░░░░░░░░░░░░░░██░░░░░░░███████
░░░░░░░░░░░░░░░░██░░░░░░░░░░█░░░░░█
░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░█
░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░█
░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░█
░░░░░░░░░░░█████████░░░░░░░░░░░░░░██
░░░░░░░░░░█▒▒▒▒▒▒▒▒███████████████▒▒█
░░░░░░░░░█▒▒███████▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒█
░░░░░░░░░█▒▒▒▒▒▒▒▒▒█████████████████
░░░░░░░░░░████████▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒█
░░░░░░░░░░░░░░░░░░██████████████████
░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░█
██░░░░░░░░░░░░░░░░░░░░░░░░░░░██
▓██░░░░░░░░░░░░░░░░░░░░░░░░██
▓▓▓███░░░░░░░░░░░░░░░░░░░░█
▓▓▓▓▓▓███░░░░░░░░░░░░░░░██
▓▓▓▓▓▓▓▓▓███████████████▓▓█
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓██
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓█
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓█
