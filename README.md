# reverse-resume-ai
AI-powered tool that optimizes resumes based on job descriptions
import React, { useState } from 'react';
import { View, Text, Button, TextInput, StyleSheet } from 'react-native';

export default function App() {
  const [taskInput, setTaskInput] = useState('');
  const [feedback, setFeedback] = useState('');

  const handleSubmit = async () => {
    const response = await fetch('http://localhost:5000/feedback', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ task_input: taskInput }),
    });

    const data = await response.json();
    setFeedback(data.feedback);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.header}>SkillQuest - Learning Challenge</Text>
      <TextInput
        style={styles.input}
        placeholder="Enter your answer here"
        value={taskInput}
        onChangeText={setTaskInput}
      />
      <Button title="Get Feedback" onPress={handleSubmit} />
      {feedback && <Text style={styles.feedback}>Feedback: {feedback}</Text>}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 16,
  },
  header: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 16,
  },
  input: {
    borderWidth: 1,
    padding: 8,
    width: '80%',
    marginBottom: 16,
  },
  feedback: {
    marginTop: 16,
    fontSize: 16,
    color: 'green',
  },
});
