import { useState, useEffect } from "react";

export default function Tracker() {
  const subjects = ["C++", "DSA", "Aptitude", "DBMS", "OS", "CN", "SQL"];
  const topics = {
    "C++": ["Basics", "OOPs", "STL"],
    "DSA": ["Arrays", "Linked List", "Sorting"],
    "Aptitude": ["Probability", "Algebra", "Puzzles"],
    "DBMS": ["Normalization", "Transactions", "Indexes"],
    "OS": ["Processes", "Memory Management", "Scheduling"],
    "CN": ["Protocols", "OSI Model", "Networking"],
    "SQL": ["Queries", "Joins", "Stored Procedures"],
    "TCS NQT Programming Logic": [
      "Data Types", "Input-Output (based on C)", "Functions and Scope", "Variables and Registers",
      "Command Line Programming", "Pointers", "Inbuilt Libraries (based on C)", "Call by value/reference",
      "Iteration", "Recursion"
    ],
    "TCS NQT Reasoning Ability": [
      "Meaningful Word Creation", "Number Series", "Data Sufficiency", "Blood Relations", "Coding-Decoding",
      "Ages", "Odd Man Out", "Distance and Directions", "Statement and Conclusion", "Seating Arrangement (Easy)",
      "Seating Arrangement (Complex)", "Analogy", "Mathematical Operational Arrangement", "Symbols and Notations"
    ],
    "TCS NQT Numerical Ability": [
      "Arrangements and Series", "P&C", "Number System", "LCM & HCF", "Percentages", "Allegations and Mixtures",
      "Probability", "Ratios, Proportion, and Averages", "Reasoning", "Work and Time", "Speed Time and Distance",
      "Geometry", "Divisibility", "Profit and Loss", "Ages", "Clocks & Calendar", "Series and Progressions",
      "Equations", "Averages", "Area, Shapes & Perimeter", "Numbers & Decimal Fractions"
    ],
    "TCS NQT Verbal Ability": [
      "Synonyms", "Antonyms", "Prepositions", "Sentence Completion", "Active and Passive Voice", "Spelling Test",
      "Spotting Errors", "Passage Completion", "Substitution", "Sentence Arrangement", "Transformation",
      "Idioms and Phrases", "Sentence Improvement", "Para Completion", "Joining Sentences",
      "Error Correction (Underlined Part)", "Error Correction (Phrase in Bold)", "Fill in the blanks"
    ]
  };
  
  const [progress, setProgress] = useState({});

  useEffect(() => {
    const savedProgress = localStorage.getItem("studyProgress");
    if (savedProgress) {
      setProgress(JSON.parse(savedProgress));
    }
  }, []);

  useEffect(() => {
    localStorage.setItem("studyProgress", JSON.stringify(progress));
  }, [progress]);

  const toggleCompletion = (subject) => {
    setProgress((prev) => ({ ...prev, [subject]: !prev[subject] }));
  };

  return (
    <div className="p-4 max-w-md mx-auto bg-meta-black text-olive-green rounded-xl shadow-md space-y-4">
      <h2 className="text-xl font-bold text-center">TCS NQT Study Tracker</h2>
      <ul>
        {Object.keys(topics).map((subject) => (
          <li key={subject} className="flex flex-col py-2 border-b">
            <div className="flex justify-between items-center">
              <span>{subject}</span>
              <input
                type="checkbox"
                checked={progress[subject] || false}
                onChange={() => toggleCompletion(subject)}
              />
            </div>
            <ul className="text-sm ml-4">
              {topics[subject].map((topic) => (
                <li key={topic}>- {topic}</li>
              ))}
            </ul>
          </li>
        ))}
      </ul>
      <h2 className="text-xl font-bold text-center mt-4">Study Timetable</h2>
      <table className="w-full border border-olive-green text-center">
        <thead>
          <tr className="bg-olive-green text-meta-black">
            <th className="border p-2">Time</th>
            <th className="border p-2">Subject</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td className="border p-2">6:00 - 7:00 AM</td>
            <td className="border p-2">C++</td>
          </tr>
          <tr>
            <td className="border p-2">7:00 - 8:00 AM</td>
            <td className="border p-2">DSA</td>
          </tr>
          <tr>
            <td className="border p-2">8:00 - 9:00 AM</td>
            <td className="border p-2">Aptitude</td>
          </tr>
          <tr>
            <td className="border p-2">9:00 - 10:00 AM</td>
            <td className="border p-2">DBMS</td>
          </tr>
        </tbody>
      </table>
    </div>
  );
}
