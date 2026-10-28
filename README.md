!pip -q install gradio

import gradio as gr

def generate_content(topic, content_type, tone):
    if not topic.strip():
        return "Please enter a topic first."

    templates = {
        "Instagram Caption": (
            f"✨ Discover something amazing about {topic}! "
            f"Share your thoughts, inspire others, and make every moment count. "
            f"# {topic.replace(' ', '')} #Inspiration"
        ),
        "Blog Introduction": (
            f"Welcome to our discussion on {topic}! "
            f"In this article, we explore its importance, key benefits, "
            f"and practical ideas to help you understand the subject better."
        ),
        "Product Description": (
            f"Introducing {topic}! Discover its features, benefits, "
            f"and how it can add value to your everyday life."
        ),
        "YouTube Description": (
            f"In today's video, we explore {topic}! "
            f"Discover useful tips and fresh ideas. Like, share, and subscribe!"
        ),
        "Motivational Post": (
            f"Every journey begins with one small step. Let {topic} "
            f"inspire you to keep learning, stay focused, and believe in yourself."
        )
    }

    return f"Tone: {tone}\n\n{templates[content_type]}"

with gr.Blocks(theme=gr.themes.Soft()) as app:
    gr.Markdown("# ✨ AI Content Generator")
    gr.Markdown("Create content easily in seconds!")

    topic = gr.Textbox(
        label="Enter Your Topic",
        placeholder="Example: Artificial Intelligence"
    )

    content_type = gr.Dropdown(
        choices=[
            "Instagram Caption",
            "Blog Introduction",
            "Product Description",
            "YouTube Description",
            "Motivational Post"
        ],
        value="Instagram Caption",
        label="Choose Content Type"
    )

    tone = gr.Radio(
        ["Professional", "Friendly", "Creative", "Casual"],
        value="Creative",
        label="Choose Tone"
    )

    generate_btn = gr.Button("✨ Generate Content")
    output = gr.Textbox(label="Generated Content", lines=7)

    generate_btn.click(
        fn=generate_content,
        inputs=[topic, content_type, tone],
        outputs=output
    )

app.launch(share=True)
