import pickle
import pandas as pd

# Load the trained model
with open("ipl_model.pkl", "rb") as file:
    model = pickle.load(file)

def predict_score(innings, overs, ballnumber, batter, bowler, batsman_run):
    """
    Function to predict total runs based on input features.
    """
    # Prepare input data
    input_data = pd.DataFrame([[innings, overs, ballnumber, batter, bowler, batsman_run]],
                              columns=['innings', 'overs', 'ballnumber', 'batter', 'bowler', 'batsman_run'])

    # Predict the total run
    predicted_score = model.predict(input_data)

    return round(predicted_score[0], 2)
