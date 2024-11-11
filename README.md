1. create a directory like
mkdir my_game
2.for open directory type
cd my_game
3. create a file inside directory 
 type nano app.py
4. paste here--
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=8080)
    press ctrl+o for save. > enter > ctrl+ x for quit
5. type nano gamelogic.py and paste this code in it..
from flask import Flask, render_template, request
import random

app = Flask(__name__)

def get_computer_choice():
    choices = ['snake', 'water', 'gun']
    choice = random.choice(choices)
    return choice

def play_game(user_choice, computer_choice):
    if user_choice == computer_choice:
        return "It's a tie!"
    if user_choice == 'snake':
        return "You win!" if computer_choice == 'water' else "Computer wins!"
    if user_choice == 'water':
        return "You win!" if computer_choice == 'gun' else "Computer wins!"
    if user_choice == 'gun':
        return "You win!" if computer_choice == 'snake' else "Computer wins!"

@app.route('/')
def index():
    return render_template('index.html')  # Load the HTML page

@app.route('/play', methods=['POST'])
def play():
    user_choice = request.form.get('user_choice')
    computer_choice = get_computer_choice()
    result = play_game(user_choice, computer_choice)
    return render_template('index.html', user_choice=user_choice, computer_choice=computer_choice, result=result)

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0',port=8080)
    
    press ctrl+o for save. > enter > ctrl+ x
6.  type mkdir templates for html file
7. now, type nano templates/index.html
paste your html code with 
this <link rel=”stylesheet” href=”{{ url_for(‘static’, filename=’styles.css’) }}”>
link in head tag if you want to add css file in it.
press ctrl+o for save. > enter > ctrl+ x for quit
8. mkdir static
9. nano static/styles.css
10. paste here your css file
11. now type--
12. python app.py
13. we got a url for local host