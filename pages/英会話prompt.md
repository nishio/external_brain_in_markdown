---
title: "英会話prompt"
---


> [@nishio](https://twitter.com/nishio/status/1652642642038259712?s=20): Whisperの結果をGPT4に食わせるのを試してるんだけど、40分の英会話を丸ごと食わせると長すぎで、受理されるくらいに切って与えてもレスポンスが途中で途切れてcontinueしてるうちに混乱してくるので、復習だと開き直って頭から刻んでいくのがいいな

英会話スクールでの会話を録音してWhisperで文字起こししたものをGPT4にきれいにさせる
prmpt

```
Given a transcription of an English conversation class between two people, please infer which person is the instructor (A) and which is the student (B) based on the conversation. The student (B) is a Japanese researcher working at a software company. Then, remove any filler words, unnecessary repetitions, false starts, and correct any spoken mistakes to create a clear and concise text. Please label the speakers as 'A', 'B', or '?'. Here is the original transcription:
```



A: Only have a conversation, or have both. Which one do you prefer today, Hilo?
B: In the previous lesson, there is a small remaining part of the lesson, so it is not comfortable. We should finish the rest of the lesson. I like it. And then we can have a conversation a lot.
A: Oh sure, let's do it, yes. So let's go to the textbook. We will go to lesson four.
B: Yes, so I will open the textbook to lesson four. Part C.
A: Part C, sure. And your last lesson was with Manlany. Did you have any questions from the last lesson?
B: Not so much, but I just tried to rephrase a lot. I tried to make more diverse discussion, so I consumed too much time to finish the lesson.
A: Oh, I see, I see. No problem, no problem.

A: So Hiro, please tell me, do you have any similar task in your office?
B: Yes, I don't have this kind of task in my company, because I am in charge of researching.
A: So do you want to talk about the real story or not real story?
B: I tried my real story.
A: Oh, good, good. Because it's not related to your work.
B: Yes.
A: I like it. So please tell me about one of your tasks from your home.
B: I have to check all the applications.
A: So let's do the role play. Hey, so I'm your manager. So Hiro, how's everything going with checking the applications?
B: I doubt if I'll be able to finish reading the whole document by 5 p.m.
A: 5 p.m.? 5 p.m. is not real. It's not real. What's the real for you?
B: In the real situation, I already finished in this morning.
A: Okay, okay. It’s just practice for the case not finishing the task. Got it. So you doubt if you... Can you say one more time?
B: Yes, I doubt if I'll be able to finish reading all the applications by 5 p.m.
A: Really? So tell me, so the deadline is 5 p.m. So do you have any reasons?
B: Yes, because I have to translate a new movie to cover our project. I was busy translating the movie subtitle of our project.
A: Oh, I see. So what should we do?
B: Yes, maybe... The deadline is 5 p.m. Because I think it is Saturday, so maybe we can extend the deadline to Sunday.
A: Can we do it?
B: Yes, because the next person to send the application results is... I mean, he is not working today. So if he is not working today, maybe we can... we have one more day. Today is Saturday, tomorrow is Sunday.
A: Can you finish it tomorrow?
B: Yes, of course.
A: Are you sure?
B: I will definitely be able to complete it by next morning.
A: Good. If you cannot finish it, what will happen?
B: Maybe...
A: Somebody will be fired.
B: No, no, no, no. But we cannot progress to the next phase. We should send the results on Monday. So, I should finish at least by tomorrow evening. Let's try to finish it.

B: This is a kind of real role play for me. In the true situation, I already finished with it this morning. I was a little nervous because there are so many documents but I already had booked the lesson.
A: Well, I think you are very efficient. You already can finish every step one by one. That's good.
B: However, this year, I tried to process it efficiently, which means I cut some features of reading. I couldn't read all documents in detail because I didn't have enough time.
A: I see. But you finished it. Congratulations.

A: So now, how do you feel?
B: I'm free. Tonight, I will relax.
A: How will you relax?
B: For example, I will take a bath for a long time.
A: That's good.


## The Origin and Difference Between Bubble Tea and Tapioca Tea
- A: Any new words or phrases you want to add?
- B: Not on this text, but I have a question. The words on the textbook are bubble tea. But you said it tapioca. I also think it is tapioca tea, so what's the difference?
- A: Actually, the original name is bubble tea. A long time ago, the shops only shook the tea, and you could see bubbles on the surface. That's the origin of bubble tea. The origin of bubble tea doesn't have tapioca, but in recent years, they decided to add tapioca. In Taiwan, if you go to a tea house or a tea shop, there is a lot of interesting colors. So, it's a very interesting part of the Taiwanese culture. So, anyway, you understand the origin. I'm very happy.



A: So we already finished this section. Do you want to try one more similar situation, or do you want to go to Lesson 5?
B: What is the role play?
A: You are in charge of a project to check out new foreign markets before launching your company's products there. Your manager has asked you for an update. You have written some notes, listing your tasks and your progress so far. Do you want to do this similar exercise?
B: Yes, they are similar.
A: Do you want to try the similar role play, or do you want to go to Lesson 5? Every student is different. Some students want to practice more. Some students say, "no, I have no time. I want to go to the next section." How about you?
B: How about to progress?
A: We can do this one now. And this can be your homework, okay? If you have time, you can try to write down your answers. And then we will check your English for you. After you finish your homework, you can give it to the counselor. And then the counselor will give it to us. We will check your English.
B: So you mean I can write the answer to sheets? And give them to the counselor?
A: Yes. The counselor will give your homework to us.
B: Okay, I understand.


A: So, is this the biggest iPad?
B: Yes, it's the largest one.
A: Why did you get the largest one?
B: I view a lot of documents, and I can see the document as a similar size of paper.
A: So maybe it's easier for you to read, right?
B: Yes, because the small font is not good for my eyes.
A: Is it very heavy?
B: Not so bad.
(Passing iPad)
A: Yeah. I like iPad very much. My iPad is an iPad mini.
B: I see. You mentioned you were weak.
A: I was very weak. Now I'm going to the gym.
B: So you can train the muscles. The heaviest iPad you need.
A: If I find this, this will be my dumbbell.
B: My wife also uses an iPad mini. Because she said it is too heavy.
A: She can go to the gym and train her muscles.
B: Okay, let's go.

B: Question.
A: Oh, I love questions.
B: I didn't say anything when I passed this to you, but I should say something, like "try this."
A: Oh, you can say, "try it." Very good, very natural English.


A: Okay, let's go to the next lesson, Lesson five. Can you please read the title?
B: Bringing bubble tea to Japan.
A: Do you know the origin of bubble tea?
B: Taiwan?
A: Yes, exactly. So we're bringing bubble tea to Japan from Taiwan. We have Tom and John. What are they talking about?
B: The goal of...
A: The goal of what?
B: Maybe where should make... I mean, where should we make a shop.
A: They are discussing about the plan of this project. Okay, so now you said where can we establish a shop, right? This is a question for me. Are you asking me a question now?
B: No, I'm describing the goal of this meeting.
A: We should try to add more words here.
B: The goal of this meeting is where we can establish a shop.
A: This is not correct English.
B: We should determine where to establish the shop.
A: Perfect, and we should say "they" instead of "we." So, "They will determine where they can open a shop."


A: Do you have any questions about this point?
B: I don't have a question, but I need to practice using the concept without thinking.

A: Do you and your wife make decisions together?
B: Yes, of course.
A: Please make a sentence.
B: My wife and I have to determine where we book a hotel when we travel. Reserve a hotel?
A: Both "book a hotel" and "reserve a hotel" are okay, but when you say "book a hotel," it can sound like you're booking the whole building, which is not what you mean.
B: So, should I say "room" instead?
A: Yes, very good. "My wife and I have to determine where we book a hotel room." That's good English.

A: Who is the final decision maker?
B: Usually, I am the final decision maker for whether to spend money or not, but I don't have a strong opinion about the hotel location or which hotel to choose. Any hotel is okay for me.
A: So you let your wife choose her favorite hotel room, and then you pay for it? You're a nice husband! Your wife must be happy.

A: Okay, what will they do after the meeting? Please use your imagination.
B: After the meeting? They will drink the bubble tea.
A: How do they feel about it?
B: I hope it's good tea. My story is crazy. I think the tapioca balls are too big. How do you say that in English?
A: Are you talking about choking on the tapioca balls?
B: Yes, maybe they will choke on the tapioca balls.


A: Let's take a look at the word. When you use the word suffocate, it is related to oxygen. Do you know oxygen?
B: Yes, I know oxygen is the air we need to live.
A: So when you say suffocate, the nuance is oxygen. Choke doesn't mean oxygen.
A: For example, the office can be suffocating if it's too stressful. But this is the second meaning. The first meaning is not enough oxygen. So, in this case, don't say suffocate. Just say they will choke on the tapioca balls and die.
B: I see.

A: Is your office like the suffocating situation? Or is there no problem with your office?
B: No problem with my office. And actually, I'm working from home.



A: Any questions?
B: Not so far.
A: Okay, cool. So, I want to highlight the important parts for you. So, Japanese people often say "remain," but in English, we like to say "didn't finish." This is a very interesting difference. And you said "long time ago," which is correct. The last one, "I try to process efficiently." But if you say "process," you need an object. So, "I try to process all documents efficiently." Or you can say, "I try to be efficient."
B: Okay, thank you.
A: Let's enter the lesson record. You chose some good words or sentences. I will type for you.
B: Yes, ...
A: All right. Okay, thank you. It's time.
B: Yes, I enjoyed talking with you.
A: Yes, it was a very interesting time for me too.


[[EnglishLesson2023-04-30-1]]
[[EnglishLesson2023-04-30-2]]
