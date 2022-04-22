# rock-paper-scissors

This is a simple game built with javascript. The game imitates the popular rock, paper scissors game.

## Table of Content 

- [Introduction](#Introduction)
- [The HTML setup](#The-HTML-Setup)
- [The CSS Setup](#The-CSS-setup)
- [The JavaScript Setup](#The-Javascript-setup)

### Introduction 

This is a simple game built with HTML, CSS, and Javascript. The game imitates the popular rock, paper scissors game.

### The HTML Setup 

The html contains a general section that wraps the entire page. Within the main section there are several other divs wrapping the different sections of the game.

The first div containes the player and computer scores both placed in seperate sub divs and initialized to 0. 

The second div is an intro to the game it contains a h2 heading that invites the visitor to play the game and a button that fades out the intro screen and fades in the
main game screen when clicked with the help of css and javascript. 

The third div is the actual game screen. I has a h2 heading that prompts the visitor to choose an option which is changed with the use of javascript to 
declare the winner of the pick. It contains two sub divs. The first one contains two images which are the icons of the hands. 
The images are later changed with javascript depending on the hand chosen by the player. The second div contains three buttons for each option, rock, paper, and scissors. 

### The CSS setup 

The css contains some basic styling for the game. The major styles are centering the player scores with flex, centering the intro screen and the game screen,
styling the buttons. Then the fadeIn and fadOut classes are added which are manipulated by javascript to fadeIn the game screen and fadeout the intro screen when 
the lets play is clicked. one interesting line of css is:

    transition: opacity 0.5s ease-in 0.5s;
which is added to both the match div and the intro screen div to creating a fading effect when fading out and fading in.
  
An animation is also added to the hands image to give a bouncing effect to the hand icons when an option is seleted. This was done with the syntax: 

    @keyframes shakePlayer {
      0% {
        transform:  rotateY(180deg) translateY(0px);
      }
      15% {
        transform:  rotateY(180deg) translateY(-50px);
      }
    }
    
 The rotateY(180deg) is used to turn the image hand icon for the player to the opposite direction of that of the computer. the translateY(0px, -50px) 
 is used to raise the hand up and down to create the bouncing effect. the same is done for the computer hands with the exclusion of the rotateY(180deg)

The animation was activated with javascript.

### The JavaScript setup

The javascript contains a function that contains several functions for different functionalities for the game. 

The first function startGame is created to fade in the game screen and fade out the intro screen when you click on a button. It first receives the button, 
the intro div and the match(game) div (with a querySelector method with their classes passed in) and assigns them to the variables named playBtn, introScreen, and match
respectively. a click eventlistener is then added to the button variable(playBtn) with a function that assigns the classes fadeOut and fadeIn(which were created in the css) to
the introScreen and the match variables respectively. 

The second function playMatch is the function that controls the option selection. It gets the three buttons for the different options using the querySelectorAll method
and assigns it to the variable *options*. It gets the hand image for the computer and the player and assigns them to their respective variables. 
to get the computer options, an array with the name computerOptions was created with each available option added as strings to the array.
a forEach loop is added to the *options* variable for each option. in the foreach loop a function was created and a variable option is passed as the argumnt of the 
function. A click event listener was then added to the argument of the function with a function that contains two variables, computerNumber and computerChoice.
computerNumber is assigned a random number between 0 and 1 like so

    const computerNumber = Math.floor(Math.random() * 3);
    
 computerChoice is then assigned the array computerOptions with the variable computerNumber as the content of the array in order to pick a random index of the 
 the array created initially. A setTimeout method is created to make the images update only after 2 secons.
 it takes two arguments, a function where the compareHands is called and the playerChoice and computerChoice are passed in as arguments. the function also updates
 the images according to the option picked by the player and randomly selected by the computer. the syntax for this is
 
    setTimeout(() => {
		  compareHands(this.textContent, computerChoice);

			//update images 
			playerHand.src = `assets/${this.textContent}.png`;
			computerHand.src = `assets/${computerChoice}.png`;
	  }, 2000);
        
 the "this" keyword selects the button selected and the textContent gets the value of the button. playerHand.src and computerHand.src updates the image by passing the 
 this.textContent and computerChoice respectively.
 
 the animation of the hand created in the css is activated in this function like so 
 
    playerHand.style.animation = "shakePlayer 2s ease";
	computerHand.style.animation = "shakeComputer 2s ease";
    
 in order to make sure the animation continues after the first time the button is clicked. a variable hands is declared and assigned the two hand imagess with
 the querySelectorAll. a forEach loop is created for each hand like so 
 
    const hands = document.querySelectorAll('.hands img');

		hands.forEach(hand => {
			hand.addEventListener('animationend', function(){
				this.style.animation = '';
			});
		});
 
 Another function created was the updateScore which updates the score of the of both the player and the computer when either wins the pick. it has two variables 
 playerScore and computerScore which gets the paragragh on the page where the score is initialized to 0 with the querySelector. the text content of the paragraph is
 then assigned to the variables pScore and cScore which were declared and initialized to 0 at the top of the function. the line of code used for this is
 
    playerScore.textContent = pScore;
		computerScore.textContent = cScore;
    
    
 The last function created was the compareHands function which is the main function to compare the results of the selection of the player with the random selection 
 of the computer and determine the winner of the pick. it takes two arguments playerCHoice and computerChoice. The first variable in the function winner gets the h2 
 with a class winners with the querySelector to be updated
 depending on the winner of the pick. several if statements are then created to compare the results of the pick. The first if statement checks if computerChoice is 
 the same as playerChoice and then updates the winner variable with a string "it is a tie".
 the second if statement checkes if the playerChoice is equal to the string rock. the another if statement is created to check if the computerChoice is equal to paper
 the textContent of the winner variable is updated to "player wins" and the pScore variable is increased by one and the updateScore function is called,
 an else if statement to check if computerChoice is equal to scissors and then the winners textcontent is updated to "computer wins" 
 and the cScore variable is increased by one and the updateScore function is called and finally a else statement that updates winners textContent to "it is tie". 
 The same is done for playerChoice equal to paper and scissors and the winner is determined based on the game rules and the winners text content is updated accordingly.
 The compareHands function is called in the playMatch function in a setTimeout method. 
 
 

