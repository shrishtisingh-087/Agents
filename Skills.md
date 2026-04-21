# AirCanvas AI - Skills & Behavior Definition

## Overview

AirCanvas AI is a gesture recognition system that interprets real-time hand movements captured via webcam to enable intuitive, air-based digital drawing. This document defines the core capabilities, rules, and behaviors of the gesture recognition engine.

---

## Core Responsibilities

The AirCanvas AI system is responsible for:

- **Hand Landmark Detection** - Identify and locate 21 hand keypoints in real-time using computer vision
- **Finger Position Tracking** - Monitor fingertip coordinates (x, y) and translate them to canvas space
- **Gesture Interpretation** - Recognize hand configurations and convert them into actionable commands
- **Drawing Action Execution** - Translate recognized gestures into canvas operations (draw, erase, select, clear)

---

## Gesture Interpretation Rules

| Gesture | Trigger Condition | Action | Priority |
|---------|-------------------|--------|----------|
| **Drawing Mode** | Index finger extended, others folded | Draw continuous line from fingertip | High |
| **Eraser Mode** | Index + Middle fingers extended, others folded | Erase content within eraser radius | High |
| **Select/Click** | Thumb + Index finger pinch (distance < threshold) | Trigger action at pinch point | Medium |
| **Clear Canvas** | Open palm (all fingers extended, spread apart) | Clear entire canvas | Medium |
| **Color Picker** | Peace sign (Index + Middle extended at 45° angle) | Open color palette | Low |
| **Reset Tracking** | Closed fist (all fingers folded) | Reset hand position anchor | Low |

---

## Tracking Logic

### Coordinate System
- **Input**: Raw hand landmark coordinates from MediaPipe (normalized 0-1)
- **Output**: Screen/Canvas coordinates (pixel-based)
- **Mapping**: Normalize webcam frame → Scale to canvas dimensions

### Position Tracking Process
