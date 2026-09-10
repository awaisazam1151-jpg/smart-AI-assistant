import streamlit as st
import time

# --- PAGE CONFIGURATION ---
st.set_page_config(
    page_title="Smart AI Study Assistant",
    page_icon="🎓",
    layout="wide",
    initial_sidebar_state="expanded"
)

# --- SESSION STATE INITIALIZATION ---
if "flashcards" not in st.session_state:
    st.session_state.flashcards = []
if "card_index" not in st.session_state:
    st.session_state.card_index = 0
if "show_answer" not in st.session_state:
    st.session_state.show_answer = False
if "quiz_score" not in st.session_state:
    st.session_state.quiz_score = 0
if "quiz_submitted" not in st.session_state:
    st.session_state.quiz_submitted = False

# --- HEADER SECTION ---
st.title("🎓 Smart AI Study Assistant")
st.caption("Your interactive mentor for active recall, concept simplification, and exam prep.")

# --- SIDEBAR: STUDY TIMER & NAVIGATION ---
with st.sidebar:
    st.header("⚙️ Study Hub")
    selected_mode = st.radio(
        "Select Assistance Mode:",
        [
            "💡 Concept Simplifier (Feynman)",
            "🃏 Automated Flashcard Deck",
            "📝 Practice Quiz Generator",
            "⏱️ Pomodoro Focus Timer"
        ]
    )
    
    st.divider()
    st.markdown("### 📊 Active Session Stats")
    st.metric("Generated Flashcards", len(st.session_state.flashcards))
    st.metric("Quiz Score", f"{st.session_state.quiz_score} pts")

# --- MODE 1: CONCEPT SIMPLIFIER ---
if selected_mode == "💡 Concept Simplifier (Feynman)":
    st.header("💡 Concept Simplifier")
    st.write("Deconstruct complex topics into plain, highly accessible language using relatable analogies.")
    
    topic = st.text_input("Enter the topic or concept you want explained:", placeholder="e.g., Recursion, Gradient Descent, Quantum Computing")
    target_level = st.selectbox("Select Target Depth:", ["Absolute Beginner (Analogy First)", "Intermediate (Core Principles)", "Advanced (Technical Breakdown)"])
    
    if st.button("🚀 Simplify Topic"):
        if topic.strip():
            with st.spinner("Breaking down concept into digestible parts..."):
                time.sleep(1) # Simulating AI processing
                
                st.subheader(f"📖 Explaining: {topic.title()}")
                
                # Formatted Educational Breakdown
                st.markdown(f"**Level:** {target_level}")
                st.info(f"**Core Concept Analogy:** Imagine **{topic}** like a factory assembly line where every worker passes a precise set of instructions to the next station.")
                
                col1, col2 = st.columns(2)
                with col1:
                    st.markdown("### 🔑 Key Takeaways")
                    st.markdown("""
                    * **Core Mechanism:** Breaks large tasks into atomic operations.
                    * **Why It Matters:** Essential for optimizing system performance and scalability.
                    * **Common Pitfalls:** Misunderstanding baseline conditions leading to infinite execution.
                    """)
                with col2:
                    st.markdown("### 🛠️ Practical Application")
                    st.markdown("""
                    1. **Step 1:** Define the boundary parameters clearly.
                    2. **Step 2:** Apply deterministic evaluation rules.
                    3. **Step 3:** Measure and verify output against ground truth.
                    """)
        else:
            st.warning("Please enter a valid topic first.")

# --- MODE 2: AUTOMATED FLASHCARD DECK ---
elif selected_mode == "🃏 Automated Flashcard Deck":
    st.header("🃏 Interactive Flashcard Generator")
    st.write("Build active recall flashcard decks to test your memory retention.")
    
    with st.form("flashcard_form"):
        st.subheader("Create New Flashcard")
        f_question = st.text_input("Question / Concept:")
        f_answer = st.text_area("Answer / Explanation:")
        submitted = st.form_submit_button("➕ Add Card to Deck")
        
        if submitted and f_question and f_answer:
            st.session_state.flashcards.append({"q": f_question, "a": f_answer})
            st.success("Flashcard added!")

    st.divider()
    
    if st.session_state.flashcards:
        st.subheader("🔁 Active Recall Deck")
        idx = st.session_state.card_index % len(st.session_state.flashcards)
        current_card = st.session_state.flashcards[idx]
        
        st.info(f"**Card {idx + 1} of {len(st.session_state.flashcards)}**")
        st.markdown(f"### ❓ Question:\n{current_card['q']}")
        
        col_a, col_b, col_c = st.columns([1, 1, 2])
        
        with col_a:
            if st.button("👁️ Toggle Answer"):
                st.session_state.show_answer = not st.session_state.show_answer
                
        with col_b:
            if st.button("▶️ Next Card"):
                st.session_state.card_index += 1
                st.session_state.show_answer = False
                st.rerun()
                
        if st.session_state.show_answer:
            st.success(f"**💡 Answer:**\n{current_card['a']}")
    else:
        st.write("No flashcards added yet. Use the form above to add your first card!")

# --- MODE 3: PRACTICE QUIZ GENERATOR ---
elif selected_mode == "📝 Practice Quiz Generator":
    st.header("📝 Diagnostic Self-Assessment Quiz")
    st.write("Evaluate your knowledge with structured assessment questions.")
    
    subject = st.selectbox("Select Subject Domain:", ["Computer Science & Logic", "Data Science & AI", "General Science"])
    
    st.subheader(f"Quiz Module: {subject}")
    
    q1 = st.radio(
        "1. Which component serves as the base condition in recursive function evaluation?",
        ["The termination check that stops further execution", "The loop iterator variable", "The global variable state"]
    )
    
    q2 = st.radio(
        "2. What is the main advantage of using deterministic rules over random selection?",
        ["Guaranteed reproducibility and 100% logical consistency", "Faster random guessing speeds", "Lower memory consumption"]
    )
    
    if st.button("📤 Submit Quiz Answers"):
        score = 0
        if q1 == "The termination check that stops further execution":
            score += 50
        if q2 == "Guaranteed reproducibility and 100% logical consistency":
            score += 50
            
        st.session_state.quiz_score = score
        st.session_state.quiz_submitted = True
        st.balloons()
        
    if st.session_state.quiz_submitted:
        st.success(f"🎯 **Your Quiz Score:** {st.session_state.quiz_score} / 100")
        if st.session_state.quiz_score == 100:
            st.write("🌟 Perfect Score! You have mastered these core concepts.")
        else:
            st.write("💡 Review the concept simplifier module to strengthen weak areas.")

# --- MODE 4: POMODORO FOCUS TIMER ---
elif selected_mode == "⏱️ Pomodoro Focus Timer":
    st.header("⏱️ Integrated Focus Timer")
    st.write("Use structured focus intervals to optimize cognitive productivity.")
    
    col_t1, col_t2 = st.columns(2)
    with col_t1:
        work_minutes = st.number_input("Focus Duration (Minutes):", min_value=1, max_value=60, value=25)
    with col_t2:
        break_minutes = st.number_input("Break Duration (Minutes):", min_value=1, max_value=30, value=5)
        
    if st.button("▶️ Start Focus Session"):
        ph = st.empty()
        total_seconds = int(work_minutes * 60)
        
        while total_seconds > 0:
            mins, secs = divmod(total_seconds, 60)
            ph.metric("⌛ Time Remaining", f"{mins:02d}:{secs:02d}")
            time.sleep(1)
            total_seconds -= 1
            
        ph.success("🔔 Focus Session Complete! Take a well-deserved break.")
