import { useState } from "react";

const SHEET_SCRIPT_URL = "https://script.google.com/macros/s/AKfycbyP58o5zHTjVU6z5uM9vjbQePn9I7iveVG0SPBsAfAkoOPwmVGQbZYqI0FOXcxtvvBY/exec";

const questions = [
  {
    id: 1,
    text: "Which learning strategy involves reviewing material at increasing intervals?",
    options: ["A. Interleaving", "B. Spaced Repetition", "C. Gamification"],
    answer: "B. Spaced Repetition",
    points: 5,
  },
  {
    id: 2,
    text: "What does retrieval practice require students to do?",
    options: ["A. Re-read notes silently", "B. Recall information without looking", "C. Copy examples repeatedly"],
    answer: "B. Recall information without looking",
    points: 5,
  },
  {
    id: 3,
    text: "According to the handbook, what should tutors use as their primary comprehension check?",
    options: ["A. Weekly tests", "B. Group discussions", "C. The Feynman Technique"],
    answer: "C. The Feynman Technique",
    points: 5,
  },
  {
    id: 4,
    text: "Before teaching a new student, tutors should first:",
    options: ["A. Assign homework", "B. Conduct a diagnostic test", "C. Start with difficult topics"],
    answer: "B. Conduct a diagnostic test",
    points: 5,
  },
  {
    id: 5,
    text: "Which of these is included in a Math diagnostic?",
    options: ["A. Vocabulary range", "B. Geometry basics", "C. Essay writing"],
    answer: "B. Geometry basics",
    points: 5,
  },
  {
    id: 6,
    text: "WAEC is especially important for students in which class in Nigeria?",
    options: ["A. JSS1", "B. Primary 6", "C. SS3"],
    answer: "C. SS3",
    points: 5,
  },
  {
    id: 7,
    text: "In the signature session structure, what comes after the warm-up?",
    options: ["A. Exit Ticket", "B. Review", "C. Preview"],
    answer: "B. Review",
    points: 5,
  },
  {
    id: 8,
    text: 'The "Exit Ticket" is used to:',
    options: ["A. End the class quickly", "B. Give homework", "C. Confirm understanding"],
    answer: "C. Confirm understanding",
    points: 5,
  },
  {
    id: 9,
    text: "Grades 3–5 students learn best through:",
    options: ["A. Long lectures", "B. Stories and games", "C. Independent research"],
    answer: "B. Stories and games",
    points: 5,
  },
  {
    id: 10,
    text: "For Grades 6–8 students, tutors should prioritize:",
    options: ["A. Competition", "B. Psychological safety", "C. Strict discipline"],
    answer: "B. Psychological safety",
    points: 5,
  },
  {
    id: 11,
    text: "Grades 9–12 students should be treated as:",
    options: ["A. Near-adults", "B. Preschoolers", "C. Beginners only"],
    answer: "A. Near-adults",
    points: 5,
  },
  {
    id: 12,
    text: "According to the handbook, tutors should avoid talking for more than:",
    options: ["A. 5 minutes without student action", "B. 15 minutes continuously", "C. 30 minutes continuously"],
    answer: "A. 5 minutes without student action",
    points: 5,
  },
  {
    id: 13,
    text: "Which tool is recommended for annotating PDFs live with students?",
    options: ["A. Canva", "B. Kami", "C. Kahoot"],
    answer: "B. Kami",
    points: 5,
  },
  {
    id: 14,
    text: "Session summaries should be sent to parents within:",
    options: ["A. 24 hours", "B. 12 hours", "C. 2 hours"],
    answer: "C. 2 hours",
    points: 5,
  },
  {
    id: 15,
    text: "A good monthly progress report should include:",
    options: ["A. Student hobbies only", "B. Topics covered and assessment scores", "C. Tutor salary details"],
    answer: "B. Topics covered and assessment scores",
    points: 5,
  },
  {
    id: 16,
    text: "What should tutors build over time?",
    options: ["A. A personal resource library", "B. A gaming account", "C. A social media fan page"],
    answer: "A. A personal resource library",
    points: 5,
  },
  {
    id: 17,
    text: "Tracking assessment scores helps tutors:",
    options: ["A. Decorate reports", "B. Show measurable progress", "C. Reduce teaching time"],
    answer: "B. Show measurable progress",
    points: 5,
  },
  {
    id: 18,
    text: "Which book is described as the best book any tutor can own?",
    options: ["A. Mindset", "B. Teach Like a Champion", "C. Make It Stick"],
    answer: "C. Make It Stick",
    points: 5,
  },
  {
    id: 19,
    text: "According to the handbook, students learn best from:",
    options: ["A. The strictest tutor", "B. The smartest tutor", "C. The tutor they trust"],
    answer: "C. The tutor they trust",
    points: 5,
  },
  {
    id: 20,
    text: "What is the greatest lesson you have learned from this handbook?",
    options: null,
    answer: null,
    points: 5,
    isOpen: true,
  },
];

const TOTAL_SCORED = 19 * 5;

const styles = `
  @import url('https://fonts.googleapis.com/css2?family=Fraunces:ital,wght@0,400;0,600;1,400&family=DM+Sans:wght@400;500;600&display=swap');

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: #f5f0e8;
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
  }

  .app {
    min-height: 100vh;
    background: #f5f0e8;
    padding: 0;
  }

  .header {
    background: #1a3a2a;
    color: #fff;
    padding: 24px 32px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .header-left h1 {
    font-family: 'Fraunces', serif;
    font-size: 22px;
    font-weight: 600;
    letter-spacing: -0.3px;
    color: #e8f5ee;
  }

  .header-left p {
    font-size: 13px;
    color: #88b89a;
    margin-top: 2px;
  }

  .header-badge {
    background: #2d5a3d;
    border: 1px solid #3d7a52;
    border-radius: 20px;
    padding: 6px 14px;
    font-size: 13px;
    color: #a8d4b6;
  }

  .progress-bar-wrap {
    background: #1a3a2a;
    padding: 0 32px 16px;
  }

  .progress-track {
    background: #2d5a3d;
    border-radius: 4px;
    height: 4px;
    width: 100%;
  }

  .progress-fill {
    background: #5cb87a;
    height: 4px;
    border-radius: 4px;
    transition: width 0.4s ease;
  }

  .progress-labels {
    display: flex;
    justify-content: space-between;
    margin-top: 6px;
  }

  .progress-labels span {
    font-size: 12px;
    color: #88b89a;
  }

  .main {
    max-width: 720px;
    margin: 0 auto;
    padding: 40px 24px;
  }

  /* Welcome screen */
  .welcome-card {
    background: #fff;
    border-radius: 16px;
    padding: 48px 40px;
    text-align: center;
    border: 1px solid #e0d8cc;
  }

  .welcome-icon {
    width: 72px;
    height: 72px;
    background: #e8f5ee;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 24px;
    font-size: 32px;
  }

  .welcome-card h2 {
    font-family: 'Fraunces', serif;
    font-size: 28px;
    color: #1a3a2a;
    margin-bottom: 12px;
    font-weight: 600;
  }

  .welcome-card p {
    color: #5a6a60;
    font-size: 15px;
    line-height: 1.6;
    max-width: 440px;
    margin: 0 auto 32px;
  }

  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
    margin-bottom: 32px;
  }

  .stat-chip {
    background: #f5f0e8;
    border-radius: 10px;
    padding: 14px;
    text-align: center;
  }

  .stat-chip .val {
    font-size: 20px;
    font-weight: 600;
    color: #1a3a2a;
    display: block;
    font-family: 'Fraunces', serif;
  }

  .stat-chip .lbl {
    font-size: 12px;
    color: #88998c;
    margin-top: 2px;
    display: block;
  }

  .form-group {
    margin-bottom: 16px;
    text-align: left;
  }

  .form-group label {
    display: block;
    font-size: 13px;
    font-weight: 500;
    color: #3a5a42;
    margin-bottom: 6px;
  }

  .form-group input {
    width: 100%;
    padding: 12px 14px;
    border: 1.5px solid #d8d0c4;
    border-radius: 10px;
    font-size: 15px;
    font-family: 'DM Sans', sans-serif;
    color: #1a3a2a;
    background: #fafaf8;
    outline: none;
    transition: border-color 0.2s;
  }

  .form-group input:focus {
    border-color: #3d7a52;
    background: #fff;
  }

  .btn-primary {
    background: #1a3a2a;
    color: #fff;
    border: none;
    border-radius: 10px;
    padding: 14px 28px;
    font-size: 15px;
    font-weight: 500;
    font-family: 'DM Sans', sans-serif;
    cursor: pointer;
    width: 100%;
    transition: background 0.2s, transform 0.1s;
  }

  .btn-primary:hover { background: #2d5a3d; }
  .btn-primary:active { transform: scale(0.98); }
  .btn-primary:disabled { background: #88998c; cursor: not-allowed; }

  /* Question card */
  .q-card {
    background: #fff;
    border-radius: 16px;
    padding: 36px;
    border: 1px solid #e0d8cc;
  }

  .q-meta {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 24px;
  }

  .q-number {
    font-size: 13px;
    font-weight: 600;
    color: #3d7a52;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .q-points {
    background: #e8f5ee;
    color: #1a5c30;
    font-size: 12px;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 20px;
  }

  .q-points.open {
    background: #fef3e2;
    color: #7a4a00;
  }

  .q-text {
    font-family: 'Fraunces', serif;
    font-size: 20px;
    color: #1a3a2a;
    line-height: 1.45;
    margin-bottom: 28px;
    font-weight: 400;
  }

  .options-list {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .option-btn {
    display: flex;
    align-items: center;
    gap: 14px;
    padding: 14px 18px;
    border: 1.5px solid #e0d8cc;
    border-radius: 10px;
    background: #fafaf8;
    cursor: pointer;
    text-align: left;
    font-size: 15px;
    font-family: 'DM Sans', sans-serif;
    color: #2a4a32;
    transition: all 0.15s;
    width: 100%;
  }

  .option-btn:hover:not(.selected):not(.correct):not(.wrong) {
    border-color: #3d7a52;
    background: #f0f8f2;
  }

  .option-letter {
    width: 28px;
    height: 28px;
    border-radius: 50%;
    background: #e8f0ec;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 13px;
    font-weight: 600;
    color: #3d7a52;
    flex-shrink: 0;
    transition: all 0.15s;
  }

  .option-btn.selected {
    border-color: #3d7a52;
    background: #e8f5ee;
  }

  .option-btn.selected .option-letter {
    background: #3d7a52;
    color: #fff;
  }

  .open-textarea {
    width: 100%;
    border: 1.5px solid #e0d8cc;
    border-radius: 10px;
    padding: 14px 16px;
    font-size: 15px;
    font-family: 'DM Sans', sans-serif;
    color: #1a3a2a;
    background: #fafaf8;
    resize: vertical;
    min-height: 130px;
    outline: none;
    line-height: 1.6;
    transition: border-color 0.2s;
  }

  .open-textarea:focus {
    border-color: #3d7a52;
    background: #fff;
  }

  .open-note {
    font-size: 13px;
    color: #88998c;
    margin-top: 10px;
    font-style: italic;
  }

  .nav-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 28px;
    gap: 12px;
  }

  .btn-secondary {
    background: transparent;
    border: 1.5px solid #c8c0b4;
    border-radius: 10px;
    padding: 12px 22px;
    font-size: 14px;
    font-weight: 500;
    font-family: 'DM Sans', sans-serif;
    color: #5a6a60;
    cursor: pointer;
    transition: all 0.15s;
  }

  .btn-secondary:hover { border-color: #3d7a52; color: #3d7a52; }

  .btn-next {
    background: #1a3a2a;
    color: #fff;
    border: none;
    border-radius: 10px;
    padding: 12px 28px;
    font-size: 14px;
    font-weight: 500;
    font-family: 'DM Sans', sans-serif;
    cursor: pointer;
    transition: background 0.2s, transform 0.1s;
    flex: 1;
  }

  .btn-next:hover { background: #2d5a3d; }
  .btn-next:active { transform: scale(0.98); }
  .btn-next:disabled { background: #88998c; cursor: not-allowed; }

  /* Results */
  .results-card {
    background: #fff;
    border-radius: 16px;
    padding: 40px 36px;
    border: 1px solid #e0d8cc;
  }

  .score-ring-wrap {
    display: flex;
    justify-content: center;
    margin-bottom: 28px;
  }

  .score-ring {
    width: 140px;
    height: 140px;
    position: relative;
  }

  .score-ring svg {
    transform: rotate(-90deg);
  }

  .score-center {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .score-number {
    font-family: 'Fraunces', serif;
    font-size: 30px;
    font-weight: 600;
    color: #1a3a2a;
  }

  .score-denom {
    font-size: 12px;
    color: #88998c;
  }

  .results-title {
    font-family: 'Fraunces', serif;
    font-size: 24px;
    color: #1a3a2a;
    text-align: center;
    margin-bottom: 6px;
  }

  .results-sub {
    text-align: center;
    color: #5a6a60;
    font-size: 14px;
    margin-bottom: 28px;
  }

  .breakdown {
    background: #f5f0e8;
    border-radius: 12px;
    padding: 20px;
    margin-bottom: 28px;
  }

  .breakdown-title {
    font-size: 13px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    color: #88998c;
    margin-bottom: 14px;
  }

  .breakdown-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
    border-bottom: 1px solid #e8e0d4;
    font-size: 14px;
    color: #3a4a3e;
  }

  .breakdown-row:last-child { border-bottom: none; }

  .breakdown-row .qtext {
    flex: 1;
    margin-right: 12px;
    line-height: 1.4;
  }

  .pill-correct {
    background: #e8f5ee;
    color: #1a5c30;
    border-radius: 20px;
    padding: 3px 10px;
    font-size: 12px;
    font-weight: 600;
    white-space: nowrap;
  }

  .pill-wrong {
    background: #fde8e8;
    color: #7a1a1a;
    border-radius: 20px;
    padding: 3px 10px;
    font-size: 12px;
    font-weight: 600;
    white-space: nowrap;
  }

  .pill-open {
    background: #fef3e2;
    color: #7a4a00;
    border-radius: 20px;
    padding: 3px 10px;
    font-size: 12px;
    font-weight: 600;
    white-space: nowrap;
  }

  .open-answer-preview {
    margin-top: 6px;
    font-size: 13px;
    color: #5a6a60;
    font-style: italic;
    padding: 8px 12px;
    background: #fff;
    border-radius: 8px;
    border: 1px solid #e0d8cc;
    line-height: 1.5;
  }

  .submit-status {
    text-align: center;
    padding: 12px;
    border-radius: 10px;
    font-size: 14px;
    margin-bottom: 16px;
  }

  .submit-status.success {
    background: #e8f5ee;
    color: #1a5c30;
  }

  .submit-status.error {
    background: #fde8e8;
    color: #7a1a1a;
  }

  .submit-status.loading {
    background: #f5f0e8;
    color: #5a6a60;
  }
`;

export default function OxroadQuiz() {
  const [phase, setPhase] = useState("welcome");
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [role, setRole] = useState("");
  const [current, setCurrent] = useState(0);
  const [answers, setAnswers] = useState({});
  const [submitStatus, setSubmitStatus] = useState(null);

  const q = questions[current];
  const progress = ((current) / questions.length) * 100;

  function calcScore() {
    let score = 0;
    questions.forEach((q) => {
      if (!q.isOpen && answers[q.id] === q.answer) score += q.points;
    });
    return score;
  }

  function handleSelect(option) {
    setAnswers((prev) => ({ ...prev, [q.id]: option }));
  }

  function handleOpenChange(val) {
    setAnswers((prev) => ({ ...prev, [q.id]: val }));
  }

  function handleNext() {
    if (current < questions.length - 1) {
      setCurrent((c) => c + 1);
    } else {
      setPhase("results");
      submitToSheets();
    }
  }

  function handlePrev() {
    if (current > 0) setCurrent((c) => c - 1);
  }

  async function submitToSheets() {
    setSubmitStatus("loading");
    const score = calcScore();
    const payload = {
      timestamp: new Date().toLocaleString("en-NG", { timeZone: "Africa/Lagos" }),
      name,
      email,
      role,
      score,
      total: TOTAL_SCORED,
      percentage: Math.round((score / TOTAL_SCORED) * 100),
      ...Object.fromEntries(
        questions.map((q, i) => [`Q${i + 1}`, answers[q.id] || "Not answered"])
      ),
    };

    try {
      await fetch(SHEET_SCRIPT_URL, {
        method: "POST",
        mode: "no-cors",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload),
      });
      setSubmitStatus("success");
    } catch {
      setSubmitStatus("error");
    }
  }

  const canProceed =
    q?.isOpen ? (answers[q.id] || "").trim().length > 10 : !!answers[q.id];

  const score = calcScore();
  const pct = Math.round((score / TOTAL_SCORED) * 100);
  const circumference = 2 * Math.PI * 52;
  const strokeDash = (pct / 100) * circumference;

  function getGrade() {
    if (pct >= 90) return "Outstanding";
    if (pct >= 75) return "Excellent";
    if (pct >= 60) return "Good";
    if (pct >= 50) return "Pass";
    return "Needs Review";
  }

  return (
    <>
      <style>{styles}</style>
      <div className="app">
        <div className="header">
          <div className="header-left">
            <h1>Oxroad Nursery & Primary School</h1>
            <p>Educator Handbook Assessment</p>
          </div>
          <div className="header-badge">📚 Educator Quiz</div>
        </div>

        {phase === "quiz" && (
          <div className="progress-bar-wrap">
            <div className="progress-track">
              <div className="progress-fill" style={{ width: `${progress}%` }} />
            </div>
            <div className="progress-labels">
              <span>Question {current + 1} of {questions.length}</span>
              <span>{Math.round(progress)}% complete</span>
            </div>
          </div>
        )}

        <div className="main">
          {phase === "welcome" && (
            <div className="welcome-card">
              <div className="welcome-icon">📖</div>
              <h2>Handbook Knowledge Assessment</h2>
              <p>
                Test your understanding of the Oxroad educator handbook. Answer 20
                questions — 19 multiple-choice and one open reflection at the end.
              </p>
              <div className="stats-row">
                <div className="stat-chip">
                  <span className="val">20</span>
                  <span className="lbl">Questions</span>
                </div>
                <div className="stat-chip">
                  <span className="val">95</span>
                  <span className="lbl">Max score</span>
                </div>
                <div className="stat-chip">
                  <span className="val">~10</span>
                  <span className="lbl">Minutes</span>
                </div>
              </div>
              <div className="form-group">
                <label>Full name *</label>
                <input
                  type="text"
                  value={name}
                  onChange={(e) => setName(e.target.value)}
                  placeholder="e.g. Adaeze Okonkwo"
                />
              </div>
              <div className="form-group">
                <label>Email address *</label>
                <input
                  type="email"
                  value={email}
                  onChange={(e) => setEmail(e.target.value)}
                  placeholder="e.g. adaeze@oxroad.edu.ng"
                />
              </div>
              <div className="form-group">
                <label>Role / Class level</label>
                <input
                  type="text"
                  value={role}
                  onChange={(e) => setRole(e.target.value)}
                  placeholder="e.g. Primary 3 Class Teacher"
                />
              </div>
              <button
                className="btn-primary"
                disabled={!name.trim() || !email.trim()}
                onClick={() => setPhase("quiz")}
              >
                Start Assessment →
              </button>
            </div>
          )}

          {phase === "quiz" && (
            <div className="q-card">
              <div className="q-meta">
                <span className="q-number">Question {current + 1}</span>
                <span className={`q-points${q.isOpen ? " open" : ""}`}>
                  {q.isOpen ? "5 pts — open reflection" : "5 points"}
                </span>
              </div>
              <p className="q-text">{q.text}</p>

              {q.isOpen ? (
                <>
                  <textarea
                    className="open-textarea"
                    value={answers[q.id] || ""}
                    onChange={(e) => handleOpenChange(e.target.value)}
                    placeholder="Write your reflection here (at least a few sentences)…"
                  />
                  <p className="open-note">
                    ✦ There is no right or wrong answer — share what genuinely resonated with you.
                  </p>
                </>
              ) : (
                <div className="options-list">
                  {q.options.map((opt) => {
                    const letter = opt[0];
                    const label = opt.slice(3);
                    const selected = answers[q.id] === opt;
                    return (
                      <button
                        key={opt}
                        className={`option-btn${selected ? " selected" : ""}`}
                        onClick={() => handleSelect(opt)}
                      >
                        <span className="option-letter">{letter}</span>
                        {label}
                      </button>
                    );
                  })}
                </div>
              )}

              <div className="nav-row">
                {current > 0 ? (
                  <button className="btn-secondary" onClick={handlePrev}>
                    ← Back
                  </button>
                ) : (
                  <div />
                )}
                <button
                  className="btn-next"
                  disabled={!canProceed}
                  onClick={handleNext}
                >
                  {current === questions.length - 1 ? "Submit Quiz ✓" : "Next →"}
                </button>
              </div>
            </div>
          )}

          {phase === "results" && (
            <div className="results-card">
              <div className="score-ring-wrap">
                <div className="score-ring">
                  <svg width="140" height="140" viewBox="0 0 140 140">
                    <circle cx="70" cy="70" r="52" fill="none" stroke="#e8e0d4" strokeWidth="10" />
                    <circle
                      cx="70" cy="70" r="52"
                      fill="none"
                      stroke={pct >= 60 ? "#3d7a52" : "#c8603a"}
                      strokeWidth="10"
                      strokeDasharray={`${strokeDash} ${circumference}`}
                      strokeLinecap="round"
                    />
                  </svg>
                  <div className="score-center">
                    <span className="score-number">{score}</span>
                    <span className="score-denom">/ {TOTAL_SCORED}</span>
                  </div>
                </div>
              </div>

              <h2 className="results-title">{getGrade()}, {name.split(" ")[0]}!</h2>
              <p className="results-sub">
                You scored {score} out of {TOTAL_SCORED} ({pct}%) on the scored questions.
              </p>

              {submitStatus === "loading" && (
                <div className="submit-status loading">⏳ Saving your results to the admin sheet…</div>
              )}
              {submitStatus === "success" && (
                <div className="submit-status success">✓ Results saved to Google Sheets successfully!</div>
              )}
              {submitStatus === "error" && (
                <div className="submit-status error">⚠ Could not reach Google Sheets — please ask admin to note your score: {score}/{TOTAL_SCORED}</div>
              )}

              <div className="breakdown">
                <p className="breakdown-title">Your Answers</p>
                {questions.map((q, i) => {
                  const ans = answers[q.id] || "Not answered";
                  const isCorrect = !q.isOpen && ans === q.answer;
                  const isWrong = !q.isOpen && ans !== q.answer;
                  return (
                    <div key={q.id}>
                      <div className="breakdown-row">
                        <span className="qtext">
                          <strong>Q{i + 1}.</strong> {q.text.length > 60 ? q.text.slice(0, 60) + "…" : q.text}
                        </span>
                        {q.isOpen ? (
                          <span className="pill-open">Reflection</span>
                        ) : isCorrect ? (
                          <span className="pill-correct">✓ Correct</span>
                        ) : (
                          <span className="pill-wrong">✗ Wrong</span>
                        )}
                      </div>
                      {q.isOpen && ans && (
                        <div className="open-answer-preview">{ans}</div>
                      )}
                      {isWrong && (
                        <div className="open-answer-preview" style={{ color: "#3d7a52" }}>
                          Correct answer: {q.answer}
                        </div>
                      )}
                    </div>
                  );
                })}
              </div>
            </div>
          )}
        </div>
      </div>
    </>
  );
}
