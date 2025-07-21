# IPL_Score_Prediction
import streamlit as st
import predict  # Import the predict function

# Streamlit UI
st.title("IPL Score Prediction")

# User Inputs
innings = st.radio("Select Innings", [1, 2])
overs = st.slider("Overs Completed", 1, 20, 10)
ballnumber = st.slider("Ball Number (1-6)", 1, 6, 3)
batter = st.number_input("Batter (Encoded Value)", min_value=0, step=1)
bowler = st.number_input("Bowler (Encoded Value)", min_value=0, step=1)
batsman_run = st.slider("Batsman's Last Ball Runs", 0, 6, 1)

# Predict button
if st.button("Predict Runs"):
    predicted_score = predict.predict_score(innings, overs, ballnumber, batter, bowler, batsman_run)
    st.success(f"Predicted Total Runs: {predicted_score}")

# Run using: `streamlit run app.py`
