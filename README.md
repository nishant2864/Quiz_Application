# CodeAlpha_Quiz_Application
# This code defines two classes, Question and Quiz, to represent individual questions and the quiz itself.  When you run the script, it will present the questions one by one, allow the user to select an answer, and then display the final score at the end of the quiz.

class Question:
    def __init__(self, text, choices, answer):
        self.text = text
        self.choices = choices
        self.answer = answer

    def check_answer(self, user_answer):
        return user_answer == self.answer

class Quiz:
    def __init__(self, questions):
        self.questions = questions
        self.score = 0
        self.question_index = 0

    def get_question(self):
        return self.questions[self.question_index]

    def display_question(self):
        question = self.get_question()
        print(f"Question {self.question_index + 1}: {question.text}")
        for i, choice in enumerate(question.choices, start=1):
            print(f"{i}. {choice}")
    
    def next_question(self):
        self.question_index += 1

    def run(self):
        for question in self.questions:
            self.display_question()
            user_answer = input("Enter the number of your answer: ")
            if user_answer.isdigit():
                user_answer = int(user_answer) - 1
                if 0 <= user_answer < len(question.choices):
                    if question.check_answer(user_answer):
                        print("Correct!\n")
                        self.score += 1
                    else:
                        print(f"Wrong. The correct answer was: {question.choices[question.answer]}\n")
                else:
                    print("Invalid choice. Please enter a valid choice.\n")
            else:
                print("Invalid input. Please enter a number.\n")
            self.next_question()
        
        print(f"Quiz completed! You scored {self.score}/{len(self.questions)}.")

if __name__ == "__main__":
    # Define your quiz questions here as Question objects
    questions = [
        Question("What is the capital of France?", ["Paris", "London", "Berlin", "Madrid"], 0),
        Question("Which planet is known as the Red Planet?", ["Earth", "Mars", "Venus", "Jupiter"], 1),
        Question("What is 7 x 8?", ["48", "56", "64", "72"], 1),
    ]

    # Create a Quiz object and run the quiz
    quiz = Quiz(questions)
    quiz.run()
