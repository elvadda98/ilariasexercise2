<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Business & Communication Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Business & Communication Terms</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>field</h3>
                    <p><strong>Definition:</strong> A particular branch of study or sphere of activity.</p>
                    <p><strong>Usage:</strong> Often used to refer to areas of expertise or professional domains.</p>
                    <p class="example"><strong>Example:</strong> "She is an expert in the field of artificial intelligence."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>task</h3>
                    <p><strong>Definition:</strong> A piece of work to be done or undertaken.</p>
                    <p><strong>Usage:</strong> Common in work, school, and project management contexts.</p>
                    <p class="example"><strong>Example:</strong> "My first task this morning is to respond to all emails."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>satisfied</h3>
                    <p><strong>Definition:</strong> Contented; pleased with what has been experienced or received.</p>
                    <p><strong>Usage:</strong> Used to express contentment with products, services, or outcomes.</p>
                    <p class="example"><strong>Example:</strong> "The customers were very satisfied with the quality of service."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>regarding</h3>
                    <p><strong>Definition:</strong> With respect to; concerning.</p>
                    <p><strong>Usage:</strong> A formal way to introduce a topic in communication.</p>
                    <p class="example"><strong>Example:</strong> "I'm writing to you regarding your recent application."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>training</h3>
                    <p><strong>Definition:</strong> The action of teaching a person or animal a particular skill or type of behavior.</p>
                    <p><strong>Usage:</strong> Common in professional development and education contexts.</p>
                    <p class="example"><strong>Example:</strong> "All new employees must complete safety training."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>for instance</h3>
                    <p><strong>Definition:</strong> As an example; for example.</p>
                    <p><strong>Usage:</strong> Used to introduce a specific example that illustrates a point.</p>
                    <p class="example"><strong>Example:</strong> "Many countries have strict environmental laws. For instance, Sweden recycles nearly all its waste."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>nuance</h3>
                    <p><strong>Definition:</strong> A subtle difference in or shade of meaning, expression, or sound.</p>
                    <p><strong>Usage:</strong> Often used when discussing subtle distinctions in language, art, or ideas.</p>
                    <p class="example"><strong>Example:</strong> "The translator struggled to capture the nuance of the original poem."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>noise</h3>
                    <p><strong>Definition:</strong> A sound, especially one that is loud or unpleasant or that causes disturbance.</p>
                    <p><strong>Usage:</strong> Can refer to literal sound or metaphorical interference in communication.</p>
                    <p class="example"><strong>Example:</strong> "The construction noise made it difficult to concentrate."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>meanwhile</h3>
                    <p><strong>Definition:</strong> At the same time; in the intervening period.</p>
                    <p><strong>Usage:</strong> Used to describe simultaneous events or actions.</p>
                    <p class="example"><strong>Example:</strong> "I'll finish this report. Meanwhile, could you prepare the presentation slides?"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>therefore</h3>
                    <p><strong>Definition:</strong> For that reason; consequently.</p>
                    <p><strong>Usage:</strong> Used to introduce a logical conclusion or result.</p>
                    <p class="example"><strong>Example:</strong> "The budget has been reduced; therefore, we need to cut some expenses."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>aim</h3>
                    <p><strong>Definition:</strong> A purpose or intention; a desired outcome.</p>
                    <p><strong>Usage:</strong> Common in goal-setting and planning contexts.</p>
                    <p class="example"><strong>Example:</strong> "Our aim is to increase customer satisfaction by 20% this year."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">field</span>
                    <span class="word-option">task</span>
                    <span class="word-option">satisfied</span>
                    <span class="word-option">regarding</span>
                    <span class="word-option">training</span>
                    <span class="word-option">for instance</span>
                    <span class="word-option">nuance</span>
                    <span class="word-option">noise</span>
                    <span class="word-option">meanwhile</span>
                    <span class="word-option">therefore</span>
                    <span class="word-option">aim</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="field" onclick="selectMatch(this)">field</div>
                    <div class="match-item" data-word="task" onclick="selectMatch(this)">task</div>
                    <div class="match-item" data-word="satisfied" onclick="selectMatch(this)">satisfied</div>
                    <div class="match-item" data-word="regarding" onclick="selectMatch(this)">regarding</div>
                    <div class="match-item" data-word="training" onclick="selectMatch(this)">training</div>
                    <div class="match-item" data-word="for instance" onclick="selectMatch(this)">for instance</div>
                    <div class="match-item" data-word="nuance" onclick="selectMatch(this)">nuance</div>
                    <div class="match-item" data-word="noise" onclick="selectMatch(this)">noise</div>
                    <div class="match-item" data-word="meanwhile" onclick="selectMatch(this)">meanwhile</div>
                    <div class="match-item" data-word="therefore" onclick="selectMatch(this)">therefore</div>
                    <div class="match-item" data-word="aim" onclick="selectMatch(this)">aim</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "field" mean in a professional context?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">An open area of land</div>
                    <div class="option" onclick="selectOption(this, true)">A particular branch of study or activity</div>
                    <div class="option" onclick="selectOption(this, false)">A sports playing area</div>
                    <div class="option" onclick="selectOption(this, false)">A background in a form</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What is a "task"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A long-term goal</div>
                    <div class="option" onclick="selectOption(this, true)">A piece of work to be done</div>
                    <div class="option" onclick="selectOption(this, false)">A difficult challenge</div>
                    <div class="option" onclick="selectOption(this, false)">A type of question</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "satisfied" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Disappointed with something</div>
                    <div class="option" onclick="selectOption(this, true)">Pleased with what has been experienced</div>
                    <div class="option" onclick="selectOption(this, false)">Neutral about something</div>
                    <div class="option" onclick="selectOption(this, false)">Angry about a situation</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: How is "regarding" used?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To express gratitude</div>
                    <div class="option" onclick="selectOption(this, true)">To introduce a topic in communication</div>
                    <div class="option" onclick="selectOption(this, false)">To show disagreement</div>
                    <div class="option" onclick="selectOption(this, false)">To indicate time</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What is "training"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of transportation</div>
                    <div class="option" onclick="selectOption(this, true)">The action of teaching a particular skill</div>
                    <div class="option" onclick="selectOption(this, false)">A long journey</div>
                    <div class="option" onclick="selectOption(this, false)">A form of punishment</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "for instance" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">At all times</div>
                    <div class="option" onclick="selectOption(this, true)">As an example</div>
                    <div class="option" onclick="selectOption(this, false)">For this reason</div>
                    <div class="option" onclick="selectOption(this, false)">In the future</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What is a "nuance"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A loud sound</div>
                    <div class="option" onclick="selectOption(this, true)">A subtle difference in meaning</div>
                    <div class="option" onclick="selectOption(this, false)">A clear distinction</div>
                    <div class="option" onclick="selectOption(this, false)">A major problem</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What does "noise" refer to?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Complete silence</div>
                    <div class="option" onclick="selectOption(this, true)">A loud or unpleasant sound</div>
                    <div class="option" onclick="selectOption(this, false)">A type of music</div>
                    <div class="option" onclick="selectOption(this, false)">A visual disturbance</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: How is "meanwhile" used?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To indicate a past event</div>
                    <div class="option" onclick="selectOption(this, true)">To describe simultaneous events</div>
                    <div class="option" onclick="selectOption(this, false)">To show cause and effect</div>
                    <div class="option" onclick="selectOption(this, false)">To express uncertainty</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What does "therefore" indicate?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A random thought</div>
                    <div class="option" onclick="selectOption(this, true)">A logical conclusion</div>
                    <div class="option" onclick="selectOption(this, false)">An unrelated idea</div>
                    <div class="option" onclick="selectOption(this, false)">A personal opinion</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 11: What is an "aim"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A random attempt</div>
                    <div class="option" onclick="selectOption(this, true)">A purpose or desired outcome</div>
                    <div class="option" onclick="selectOption(this, false)">A type of weapon</div>
                    <div class="option" onclick="selectOption(this, false)">A measurement of accuracy</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "field", text: "A particular branch of study or activity" },
            { meaning: "task", text: "A piece of work to be done" },
            { meaning: "satisfied", text: "Pleased with what has been experienced" },
            { meaning: "regarding", text: "With respect to; concerning" },
            { meaning: "training", text: "The action of teaching a particular skill" },
            { meaning: "for instance", text: "As an example; for example" },
            { meaning: "nuance", text: "A subtle difference in meaning" },
            { meaning: "noise", text: "A loud or unpleasant sound" },
            { meaning: "meanwhile", text: "At the same time; in the intervening period" },
            { meaning: "therefore", text: "For that reason; consequently" },
            { meaning: "aim", text: "A purpose or desired outcome" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "She is an expert in the <input type='text' class='fill-blank' data-answer='field' placeholder='answer'> of artificial intelligence.", answer: "field" },
            { text: "My first <input type='text' class='fill-blank' data-answer='task' placeholder='answer'> this morning is to respond to all emails.", answer: "task" },
            { text: "The customers were very <input type='text' class='fill-blank' data-answer='satisfied' placeholder='answer'> with the quality of service.", answer: "satisfied" },
            { text: "I'm writing to you <input type='text' class='fill-blank' data-answer='regarding' placeholder='answer'> your recent application.", answer: "regarding" },
            { text: "All new employees must complete safety <input type='text' class='fill-blank' data-answer='training' placeholder='answer'>.", answer: "training" },
            { text: "Many countries have strict environmental laws. <input type='text' class='fill-blank' data-answer='for instance' placeholder='answer'>, Sweden recycles nearly all its waste.", answer: "for instance" },
            { text: "The translator struggled to capture the <input type='text' class='fill-blank' data-answer='nuance' placeholder='answer'> of the original poem.", answer: "nuance" },
            { text: "The construction <input type='text' class='fill-blank' data-answer='noise' placeholder='answer'> made it difficult to concentrate.", answer: "noise" },
            { text: "I'll finish this report. <input type='text' class='fill-blank' data-answer='meanwhile' placeholder='answer'>, could you prepare the presentation slides?", answer: "meanwhile" },
            { text: "The budget has been reduced; <input type='text' class='fill-blank' data-answer='therefore' placeholder='answer'>, we need to cut some expenses.", answer: "therefore" },
            { text: "Our <input type='text' class='fill-blank' data-answer='aim' placeholder='answer'> is to increase customer satisfaction by 20% this year.", answer: "aim" },
            { text: "There are many programming languages to learn, <input type='text' class='fill-blank' data-answer='for instance' placeholder='answer'> Python, JavaScript, and Java.", answer: "for instance" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
