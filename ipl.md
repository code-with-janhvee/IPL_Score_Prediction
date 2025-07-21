import tkinter as tk
from tkinter import messagebox
import pickle
import numpy as np

# Load the trained model
try:
    with open("ipl_model.pkl", "rb") as file:
        model = pickle.load(file)
except FileNotFoundError:
    messagebox.showerror("Error", "Model file not found! Train and save the model first.")
    exit()

# Function to predict score
def predict_score():
    try:
        # Get input values from entry fields
        innings = int(entry_innings.get())
        over = int(entry_over.get())
        ball = int(entry_ball.get())
        batter = int(entry_batter.get())
        bowler = int(entry_bowler.get())
        last_runs = int(entry_last_runs.get())

        # Prepare the input for prediction
        input_features = np.array([[innings, over, ball, batter, bowler, last_runs]])
        
        # Predict the score
        predicted_score = model.predict(input_features)

        # Display the predicted score
        label_result.config(text=f"Predicted Total Runs: {predicted_score[0]:.2f}")

    except ValueError:
        messagebox.showerror("Input Error", "Please enter valid numerical values!")
    except Exception as e:
        messagebox.showerror("Error", f"An error occurred: {e}")

# Create GUI window
root = tk.Tk()
root.title("IPL Score Prediction")

# Input Fields
tk.Label(root, text="Enter Innings (1 or 2):").pack()
entry_innings = tk.Entry(root)
entry_innings.pack()

tk.Label(root, text="Enter Current Over:").pack()
entry_over = tk.Entry(root)
entry_over.pack()

tk.Label(root, text="Enter Ball Number (1-6):").pack()
entry_ball = tk.Entry(root)
entry_ball.pack()

tk.Label(root, text="Enter Batter (Encoded Value):").pack()
entry_batter = tk.Entry(root)
entry_batter.pack()

tk.Label(root, text="Enter Bowler (Encoded Value):").pack()
entry_bowler = tk.Entry(root)
entry_bowler.pack()

tk.Label(root, text="Enter Batsman's Last Ball Runs:").pack()
entry_last_runs = tk.Entry(root)
entry_last_runs.pack()

# Predict Button
btn_predict = tk.Button(root, text="Predict Score", command=predict_score)
btn_predict.pack()

# Result Label
label_result = tk.Label(root, text="Predicted Total Runs: ")
label_result.pack()

# Run the GUI
root.mainloop()
