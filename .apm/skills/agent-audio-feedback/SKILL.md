---
name: agent-audio-feedback
description: Provide optional text-to-speech status announcements for meaningful agent workflow transitions. Use only when the user explicitly enables audio feedback, TTS, spoken progress updates, or agent status narration.
---

# Agent Audio Feedback

Audio feedback is an explicit opt-in state. Start with TTS off; begin speaking
only after the user asks for TTS, audio feedback, spoken progress updates, or
agent status narration.

While TTS is enabled, announce meaningful transitions with a short
text-to-speech message, then keep working normally.

## When To Speak

Speak at meaningful changes of action, approach, or intent:

- Starting an investigation or switching tasks.
- Narrowing or changing hypotheses.
- Preparing edits or running commands.
- Verifying results or debugging failures.
- Sending a visible progress update to the user.

Do not announce every small file read or search. Use audio only when it helps
the user follow a meaningful transition.

## Message Rules

- Loading this skill does not change the opt-in state.
- If the user explicitly says to disable TTS, stop using audio feedback until
  they explicitly enable it again.
- Keep messages short, under 5 words when possible.
- Summarize the observable action or intent, not hidden reasoning.
- Do not speak secrets, credentials, PII, raw prompts, or long code/file content.
- If TTS is unavailable or fails, continue the task and mention the failure once.

## Windows PowerShell

Use the bundled script from this skill:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "<skill_dir>/scripts/cursor-tts.ps1" "Investigating tests"
```

Resolve `<skill_dir>` to the directory containing this `SKILL.md`. When installed
by APM, this is typically a directory like `.agents/skills/agent-audio-feedback`.

## Other Platforms

```bash
# macOS
say "Investigating tests" &

# Linux
espeak-ng "Investigating tests" &
```
