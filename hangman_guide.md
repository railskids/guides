So now that we have cloud9 set up let's get to our first Ruby app. 

Before we get much further, though, here's the 5 second overview of what Ruby is and what Ruby on Rails is (we are called Rails Kids after all). 

**Ruby** is the actual programming language used to code with. It provides what we in the computer world call the "**syntax**", which is just a fancy word to tell us what words we need to type in our code to tell Ruby what to do. 

**Ruby on Rails**, or just **Rails** for short, is what we call a "**framework**", which is another fancy word that basically means that it provides a lot of stuff all ready to go that we build on top of. If you've ever seen a house being built you know that there's a lot of work that goes into the foundation, the big concrete block or platform that you don't actually even see when the house is built, but without it the house would fall apart. Well, Ruby on Rails provides this foundation for us to build web applications in a strong way so we don't have to start from scratch each time. 

Anyway enough chit-chat, let's get on to the code!  Even though we're called RailsKids, we're just going to start with a couple of Ruby apps (without the Rails) to get us going. 

Open up cloud9 and create a new file. 

Let's call it helloworld.rb

Then in the file type in **puts ‘hello world’**

Now save it and run the file. 

What do you see in the box down the bottom (which we call the **console**)?  You're probably saying - "that's it, that's all it does?" and our answer is “Yep!”  For some strange reason that is the first thing that any coder codes when they're learning a new language. Often a different language takes so much longer to get to this point, but with Ruby it just works, quickly. 

Never fear, though, we're going to take it a step further now and do something a bit more fun. Who's up for a game of hangman?

Create a new file

Call it hangman.rb

Now type this code in line by line - we'll explain it along the way. And while we don't know if you're copying and pasting or not, trust me when I say that you will get so much better at coding more quickly if you type it yourself - so do yourself a favour and get your finger muscles exercising on the keyboard!

We're using some code we found here .. 

[https://gist.github.com/ajaxray/3106239](https://gist.github.com/ajaxray/3106239)

*=begin Hangman
  
  A simple word game
  Date: today's date*

* Author: your name*

*=end
*this is a comment block that is good practice to put at the top of your code. It just means that when you come back to it years later you remember what it was for. 

*words = %w"learning lollipop education image computer mobile january february friday flower beauty light earth machine book
news yahoo google internet bangladesh india america cricket football friday sunday sunny"
*

this is the list of words that you will be guessing from. The %w out the front means to split each of the words, separated by a space, into their own "buckets" in an **array **could *words. *

You'll be using arrays a lot so it's worth spending a bit of time now to understand them. Whenever you want to use a list of something you generally store them in some form of an array (there are other arrays called maps and hashes but we'll get to them later).  We'll see further down what we end up using this array for. 

*total_chances = 5
wrong_try = 0
right_guess = ''
*
Here is where we **initialise** our **variables. **If you've used variables in scratch you'd be familiar with doing this. This is just the Ruby way of doing it. In Ruby and most other languages variable names can't have spaces, so we use the **underscore _ **character instead. (It isn't actually wrong if you don't use an underscore, but there are particular ways that Ruby coders like to do things (like the 2 space tabs we set up in Cloud9) that just helps read each other's code - this is called a **naming** **convention**)

We'll be using these variables further down too. 

hanged = <<HANG
 +---+-
 |   |
 |   0
 |   |\\
 |   /\\
-+----------
HANG

survibed = <<WIN
   (@)
  ^\\|
    |/^
____|_____
WIN

These 2 variables are the fancy "ascii art" that shows when you either lose or win.  Now you’ll notice a spelling mistake in the variable name, we’ll leave it as it is for now, but we’ll come back later to fix it up. 


word = words[rand(words.length) - 1]

This chooses a random word from the total array of words.

def get_placeholder sample_word, guessed_words
  placeholder = ''
  sample_word.chars { |char| 
    placeholder += (guessed_words.include? char)? char : '#'
  }

  placeholder
end

This is a tricky part of the code .. 

def - defines a function that can be user over and over again so we don’t need to keep rewriting the same thing - this is one of the principles of Ruby - Don’t Repeat Yourself (DRY)

get_placeholder - the name of the function

sample_word, guessed_words - the "parameters" to the function, or the bits of information that the function needs 

puts `clear`
puts 'Guess what is:'+ get_placeholder(word, '')

while true
  print "Enter word [#{total_chances - wrong_try} chances left]:"

  char = gets.chomp
  puts `clear`
  
  if word.include? char

    if(right_guess.include? char)
      puts char + ' is already given and accepted.'
      puts 'Try another: ' + get_placeholder(word, right_guess)
    else
      right_guess = right_guess + char
      placeholder = get_placeholder(word, right_guess)

      puts 'Great! ' + placeholder
    end

    unless placeholder.include? '#'
      puts "WELL DONE!! YOU SURVIVED"
      puts survibed
      break
    end
  else
    puts "Sorry! The word dosen't contains '#{char}'"
    wrong_try += 1

    if (wrong_try == total_chances)
      puts "YOU HANGED!"
      puts hanged
      break
    else
      puts 'Try another: ' + get_placeholder(word, right_guess)
    end
  end

End

EXTENSION

Fix "survibed" variable name (refactor)

Add more words manually

Change the ascii art

Connect to a dictionary to get a random word from the internet (advanced)

 

