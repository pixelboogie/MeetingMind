# MeetingMind

## Description
**MeetingMind** is an advanced AI application designed to enhance the efficiency of capturing and summarizing business meetings. The application integrates OpenAI's Whisper technology for accurate speech-to-text transcription and IBM Watson's AI to analyze and extract key points from the transcribed text. The entire process is made accessible through a user-friendly interface developed using Hugging Face's Gradio, making it easy to use even for non-technical users.

This project demonstrates the practical application of cutting-edge AI technologies to create comprehensive solutions that address real-world needs in corporate and educational settings.

## Features
- **Speech-to-Text Transcription**: Utilizes OpenAI's Whisper model to convert spoken language into accurate text.
- **Summarization**: Integrates IBM Watson's AI to process transcriptions and extract significant insights and summaries from meetings.
- **User-Friendly Interface**: Built with Hugging Face Gradio, providing an intuitive web interface for easy interaction with the application.
- **Real-Time Output Presentation**: Displays transcribed and summarized content directly within the Gradio interface.
- **Environment Setup**: Configured for seamless deployment using Python virtual environments and necessary libraries.

## Installation

### Prerequisites
- Python 3.7 or higher
- FFmpeg installed on your system
- API keys for OpenAI Whisper and IBM Watson AI services

### Steps
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/MeetingMind.git
   cd MeetingMind

2. **Set Up a Virtual Environment:**

    Create and activate a Python virtual environment:

        python -m venv env
        source env/bin/activate  # On Windows use `env\Scripts\activate`

3. **Install Required Libraries:**

    Install the necessary Python packages:

        pip install -r requirements.txt

4. **Install FFmpeg:**

    Follow the instructions to install FFmpeg on your system. This is required for handling audio files.

5. **Set Up Environment Variables:**

    Create a .env file in the project root directory and add your API keys:

        OPENAI_API_KEY=your_openai_api_key_here
        IBM_WATSON_API_KEY=your_ibm_watson_api_key_here

6. **Run the Application:**

    Start the application using the following command:

        python app.py

7. **Access the Interface:**

    Open your web browser and navigate to the local server address provided by Gradio (usually http://localhost:7860) to interact with the MeetingMind application.

## Usage

1. **Upload an Audio File:** Use the Gradio interface to upload an audio recording of a meeting.
2. **Transcription:** The application will use OpenAI's Whisper model to transcribe the spoken content into text.
3. **Summarization:** IBM Watson AI processes the transcribed text to generate concise summaries of the meeting's key points.
4. **View Results:** The transcription and summarized key points are displayed in the Gradio interface for easy review.

## Example Code

Here's an example of how the transcription and summarization functionality is implemented:

    import openai
    import gradio as gr
    from ibm_watson import NaturalLanguageUnderstandingV1
    from ibm_watson.natural_language_understanding_v1 import Features, KeywordsOptions

    def transcribe_audio(audio_file):
        # Transcribe audio to text using Whisper
        transcript = openai.Whisper.transcribe(audio_file)
        return transcript

    def summarize_text(transcript):
        # Summarize text using IBM Watson
        nlu = NaturalLanguageUnderstandingV1(
            version='2021-08-01',
            iam_apikey='your_ibm_watson_api_key_here',
            url='your_ibm_watson_url_here'
        )
        response = nlu.analyze(
            text=transcript,
            features=Features(keywords=KeywordsOptions(sentiment=True, emotion=True, limit=5))
        ).get_result()
        
        return response

    def process_meeting(audio_file):
        transcript = transcribe_audio(audio_file)
        summary = summarize_text(transcript)
        return transcript, summary


## License

This project is licensed under the MIT License. See the LICENSE file for more information.
