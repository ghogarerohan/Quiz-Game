var questions = [{
    question: "Which crop is sown on the largest area in India?",
    choices: ["Rice","Wheat","Sugarcane","Maize"],
    correctAnswer : 0
    }, {
        question: "Which of the following is the outstanding contribution of Scientist Aneriko Fermi in Physics?",
        choices: ["Nuclear Furnace or Bath","Laws of Motion","Discovery of Calculus","Parasite"],
        correctAnswer : 0  
    }, { 
        question : "Which of the following are components of Central Processing Unit (CPU)?",
        choices: ["Arithmetic logic unit, Mouse","Arithmetic logic unit, Control unit","Arithmetic logic unit, Integrated Circuits","Control Unit, Monitor"],
        correctAnswer : 1

    },{
        question : "National Income estimates in India are prepared by",
        choices : ["Planning Commission", "Reserve Bank of India","Central statistical organization"," Indian Statistical Institute"],
        correctAnswer : 2
    }, {
        question : "Who established the Mughal Dynasty?",
        choices : ["Akbar", "Babur","Humayun","Bahadur Shah"],
        correctAnswer : 1
    }, {
        question : "Which is the largest producer and exporter of Rubber in the world?",
        choices : ["India", "Thailand","Sri Lanka","China"],
        correctAnswer : 1
    }, {
        question : "Which one is not a harvest festival in India?",
        choices : ["Onam", "Lohri","Ugadi","Holi"],
        correctAnswer : 3
    },{
        question : "2010 Commonwealth Games held in?",
        choices : ["Canada", "India","Britain","Malaysia"],
        correctAnswer : 1
    },{
        question : "_____________ is for the contribution to Literature?",
        choices : ["Booker Prize", "Moorti Devi Award","Saraswati Samman","Jnapith Award","All of these"],
        correctAnswer : 4
    },{
        question : "The first high-level programming was ..........",
        choices : ["COBOL", "FORTRAN","LISP","Pascal"],
        correctAnswer : 1
    },{
        question : "India is located on which part of Indo-Australian Plate",
        choices : ["Northern", "Sothern","Eastern","Western"],
        correctAnswer : 0
    },{
        question : "Which of the following countries are separated by the Strait of Gibraltar?",
        choices : ["Portugal and Morocco", "Algeria and Spain","Morroco and Spain","Algeria and Portugal"],
        correctAnswer : 0
    },]

    var currentQuestion = 0;
    var correctAnswers = 0;
    var quizOver = false;
    
    $(document).ready(function () {
    
        // Display the first question
        displayCurrentQuestion();
        $(this).find(".quizMessage").hide();
    
        // On clicking next, display the next question
        $(this).find(".nextButton").on("click", function () {
            if (!quizOver) {
    
                value = $("input[type='radio']:checked").val();
    
                if (value == undefined) {
                    $(document).find(".quizMessage").text("Please select an answer");
                    $(document).find(".quizMessage").show();
                } else {
                    // TODO: Remove any message -> not sure if this is efficient to call this each time....
                    $(document).find(".quizMessage").hide();
    
                    if (value == questions[currentQuestion].correctAnswer) {
                        correctAnswers++; // storing correct answers
                    }
    
                    currentQuestion++; // Since we have already displayed the first question on DOM ready
                    if (currentQuestion < questions.length) {
                        displayCurrentQuestion();
                    } else {
                        displayScore();
                        //                    $(document).find(".nextButton").toggle();
                        //                    $(document).find(".playAgainButton").toggle();
                        // Change the text in the next button to ask if user wants to play again
                        $(document).find(".nextButton").text("Play Again?");
                        quizOver = true;
                    }
                }
            } else { // quiz is over and clicked the next button (which now displays 'Play Again?'
                quizOver = false;
                $(document).find(".nextButton").text("Next Question");
                resetQuiz();
                displayCurrentQuestion();
                hideScore();
            }
        });
    
    });
    
    // This displays the current question AND the choices
    function displayCurrentQuestion() {
    
        console.log("In display current Question");
    
        var question = questions[currentQuestion].question;
        var questionClass = $(document).find(".quizContainer > .question");
        var choiceList = $(document).find(".quizContainer > .choiceList");
        var numChoices = questions[currentQuestion].choices.length;
    
        // Set the questionClass text to the current question
        $(questionClass).text(question);
    
        // Remove all current <li> elements (if any)
        $(choiceList).find("li").remove();
    
        var choice;
        for (i = 0; i < numChoices; i++) {
            choice = questions[currentQuestion].choices[i];
            $('<li><input type="radio" value=' + i + ' name="dynradio" />' + choice + '</li>').appendTo(choiceList);
        }
    }
    
    function resetQuiz() {
        currentQuestion = 0;
        correctAnswers = 0;
        hideScore();
    }
    
    function displayScore() {
        $(document).find(".quizContainer > .result").text("You scored: " + correctAnswers + " out of: " + questions.length);
        $(document).find(".quizContainer > .result").show();
    }
    
    function hideScore() {
        $(document).find(".result").hide();
    }