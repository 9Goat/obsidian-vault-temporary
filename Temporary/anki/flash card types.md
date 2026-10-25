there are several types of flashcards that includes:

## Basic

With basic cards you have:![[Pasted image 20241117092439.png|lp right]]

1. **Front**: which will be the main question
2. **Back**: which will be the answer of our question *front*

**Note**: To navigate from front to back without moving our mouse just click '**Tab**'

## Reverse (rarely used)

reverse is essentially very similar to basic except that when you type your front and back you get 2 cards.But how?

1. the first card will be a basic card
2. the second will be a reverse (meaning the front question will be the back answer and the opposite is true)

**When to use it?** if you have a question that can also be an answer use reverse (mostly used in definitions)

## Cloze deletion

Creates 'fill the gap' type of question here is how it works:

- you only have front text . In that front text you can select what words you would like to guess/try to fill the gap by clicking on the cloze button or pressing the hotkey **'Ctrl+Shift+C'**![[Pasted image 20241117095017.png|lp right]]
- you can select more than 1 section and each of those sections will have an order number attached to it
![[Pasted image 20241117095956.png]]
- from 1 to N:
	- if multiple sections have the same order you will be asked to fill multiple gaps in 1 question\
	- else if multiple sections have different order numbers that will result in multiple cards equal to the number of different orders where you have to fill the gap for each section separately
- you can add hints for each section by using this **Syntax:**`{{c1::text::hint}}`  *c1 refers to order 1*
- you can also add context to your card after revealing the answer by filling **'Back extra'** text (useful for explaining the answer)

## Image conclusion

Lets use create an image based flashcard where you can hide parts of the image and try to guess them here is a breakdown of how it works:

1. you select an image
![[Pasted image 20241117104054.png|lp right]]
2. sensor the parts of the image that you want to guess when questioned
3. **optionally**: you can add text to add more context to the image
4. select the type of image conclusion there are main types(only matters if you have multiple parts of the image hidden):
	- **Hide one guess one**: only hides one part and you have to guess it (the rest are exposed)
		- **Example:** you want to remember a country name based on other countries around it
	- **Hide all guess one**:everything is hidden and you have to guess one of them (the one you have to guess will be highlighted)
		- **Example:** you want to remember a country name based on its location/shape not other countries around it\
5. after clicking done you will get a number of cards equal to the number of hidden parts and each card will test you specific hidden part

## Basic (type in the answer)

the same as [[flash card types#Basic]] except that instead of guessing the answer you have to type it manually and after revealing , anki will tell you how close it was to the answer.