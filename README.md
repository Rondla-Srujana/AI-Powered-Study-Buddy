# AI-Powered-Study-Buddy
import streamlit as st
from transformers import pipeline

# Load AI models
summarizer = pipeline("summarization")
qa_model = pipeline("text2text-generation")

# Title
st.title("📚 AI-Powered Study Buddy")

# Menu
option = st.selectbox("Choose Function", 
                     ["Explain Topic", "Summarize Notes", "Generate Quiz"])

# User input
user_input = st.text_area("Enter your topic or text:")

# Explain Topic
if option == "Explain Topic":
    if st.button("Explain"):
        prompt = f"Explain this in simple words: {user_input}"
        result = qa_model(prompt, max_length=100)
        st.write("📖 Explanation:")
        st.write(result[0]['generated_text'])

# Summarize Notes
elif option == "Summarize Notes":
    if st.button("Summarize"):
        summary = summarizer(user_input, max_length=100, min_length=30)
        st.write("📝 Summary:")
        st.write(summary[0]['summary_text'])

# Generate Quiz
elif option == "Generate Quiz":
    if st.button("Generate"):
        prompt = f"Generate 3 simple quiz questions from this: {user_input}"
        result = qa_model(prompt, max_length=150)
        st.write("❓ Quiz Questions:")
        st.write(result[0]['generated_text'])
