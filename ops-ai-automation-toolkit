import streamlit as st
from openai import OpenAI
import os
from dotenv import load_dotenv

# 1. Security Configuration
load_dotenv()
api_key = os.getenv("OPENAI_API_KEY")
client = OpenAI(api_key=api_key)

# 2. Visual Interface (Clean & Professional)
st.set_page_config(page_title="AI Operations Toolkit", page_icon="⚙️")
st.title("AI Operations & Data Toolkit")
st.markdown("### Technical Asset Transformer")
st.write("This utility optimizes engineering productivity by structuring raw technical data into high-quality Markdown for documentation and AI consumption.")

# 3. File Upload Section
uploaded_file = st.file_uploader("Upload technical logs, audit reports, or raw text (.txt)", type="txt")

if uploaded_file is not None:
    # Reading the uploaded content
    raw_content = uploaded_file.getvalue().decode("utf-8")
    
    with st.expander("Review Original Data"):
        st.text(raw_content)

    # 4. Action Button
    if st.button("Generate Structured Output"):
        with st.spinner("Processing technical architecture..."):
            try:
                # Engineering-focused System Prompt
                system_instruction = (
                    "You are an expert Technical Architect. Your goal is to transform raw operational logs "
                    "or messy documentation into a professional, clean Markdown file. Use clear headers, "
                    "bullet points, and tables. Ensure the output is optimized for data integrity and "
                    "team collaboration."
                )
                
                response = client.chat.completions.create(
                    model="gpt-4o-mini", 
                    messages=[
                        {"role": "system", "content": system_instruction},
                        {"role": "user", "content": raw_content}
                    ]
                )
                
                # Output handling
                final_markdown = response.choices[0].message.content
                st.success("Documentation Structure Completed!")
                
                # Tabs for different views
                tab1, tab2 = st.tabs(["Preview", "Raw Markdown"])
                
                with tab1:
                    st.markdown(final_markdown)
                
                with tab2:
                    st.code(final_markdown, language="markdown")
                
            except Exception as e:
                st.error(f"Operational Error: {e}")
