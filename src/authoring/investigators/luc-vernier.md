# HeroTerminal Authoring: The Luc Vernier Protocols

> **NOTE TO AUTHORS:**
> This guide defines the specific narrative constraints, tone, and rules for cases featuring **Luc Vernier** as the lead investigator.
>
> HeroTerminal is a platform designed to host multiple investigators, each with their own unique methods, locations, and rules. **If you are creating a new investigator from scratch, these specific rules (Lyon, the Peugeot, Claire) do not apply to you.**
>
> However, if you are writing a case for Luc Vernier, treat this document as law. To maintain consistency in his storyline, you must inhabit his world completely.

---

## Welcome to Luc's World

In Luc Vernier's corner of HeroTerminal, we aren't just creating puzzles; we're writing interactive noir grounded in the Rhône-Alpes region of France.

This document outlines how to capture his voice, build his world, and structure his investigations.

## 1. The Golden Rule: The Place is the Storyteller & The Teacher

The setting is typically Lyon, France, and its surrounding regions. Use real street names, districts (Vieux Lyon, La Part-Dieu), and local culture to ground the story.

We don't create disconnected databases. Each case is a journey.

When the player opens a folder (Lead), they are physically located at a specific place (e.g., Vieux Lyon, The Docks, or The Abandoned Warehouse).

The goal is for the player to experience the atmosphere and learn something real and specific about the location in every single Lead.

The "Hyper-Local" Mandate: The player must walk away from every folder knowing a secret about that place—a historical quirk, a geological fact, or a local legend—that they didn't know before. This isn't a Wikipedia entry; it's "insider knowledge" filtered through Luc's noir lens.

### 1.1. Luc’s Territory (Geographic Scope)
Luc is based in Lyon, but his cases take him anywhere within a roughly 4-hour driving radius. This includes:

*   **Lyon & Surroundings:** The industrial heart.
*   **Switzerland (Geneva):** High finance, cold efficiency.
*   **The South (Montpellier/Marseille):** Heat, ports, and traffic.
*   **The Alps (Grenoble/Annecy):** Isolation and mountains.

## 2. Case Structure (The Lead Chain)

A case always follows a linear, geographical progression. Luc Vernier doesn't "teleport." He drives his old Peugeot. The journey between Lead 01 and Lead 02 is part of the story. Use this travel time to describe the changing landscape, the traffic on the A7 autoroute, or Luc's complaints about Swiss border control. The travel builds anticipation for the next location.

**Briefing (Claire) ➔ Lead 01 (Location A) ➔ Lead 02 (Location B) ➔ Lead 03 (Final Destination)**

*   **Lead 01:** Starting point (e.g., crime scene).
*   **The Bridge:** A clue that points to the next location.
*   **Lead 02:** The pursuit (e.g., witness or hidden location).
*   **Lead 03:** The resolution (e.g., arrest or discovery).

## 3. Folder Content: What's on the Desk?

Each Lead folder the player opens must contain a mix of the following four types of data:

*   **🔹 A. The Flavor (Atmosphere & Lore)**
    *   **Role:** To build the world and teach the player something.
    *   **Examples:** Old newspaper articles, historical documents about the building, a cafe menu, a police report about the weather.
    *   **Note:** This does not have to be directly related to the crime, but must be connected to the location.

*   **🔹 B. The Hard Evidence (The Technical Puzzle)**
    *   **Role:** The actual puzzle that needs to be solved.
    *   **Examples:** Server logs, access logs, IP addresses, license plates, bank transactions.
    *   **Note:** The solution must be an objective fact (Fact-based logic).

*   **🔹 C. The Soft Evidence (The Human Element)**
    *   **Role:** To give the story heart and show human fallibility.
    *   **Examples:** An audio recording of a witness, email correspondence, call records, a note.
    *   **Note:** People lie or misremember. Computers rarely lie.

*   **🔹 D. The Bridge**
    *   **Role:** To tell Luc (and the player) where to go next.
    *   **Examples:** Luc's Note confirming the destination and complaining about traffic.

> ### Example Scenario: The Docks
>
> **A. Flavor:** A scanned pamphlet about the history of Lyon's silk trade routes.
>
> **B. Hard Evidence:** A shipping container manifest (CSV file) with weight discrepancies.
>
> **C. Soft Evidence:** An audio recording of a nervous crane operator trying to explain the weight difference.
>
> **D. Bridge:** Luc's note: "The manifest mentions a warehouse in the industrial zone. The crane operator is lying, but the paperwork points north. Time to drive."

## 4. Character Voices (Tone of Voice)

The communication between Claire and Luc is the heart of the "meta-story."

| Character | Role | Style & Wording | Example |
| :--- | :--- | :--- | :--- |
| **Claire Vernier** | The Handler | Corporate Speak. Uses buzzwords, is cold, professional, and focuses on results. | "We need to align on deliverables. Circle back to me when you have actionable intel." |
| **Luc Vernier** | The Detective | Noir & Analog. Sarcastic, tired, hates technology, loves coffee and his old car. | "The server room smelled like ozone and cheap cologne. I miss the days of paper files." |

### How Luc Thinks (Teaching via Monologue)
Luc doesn't just list facts in his notes; he synthesizes them. He looks for anomalies. When you write Luc's notes, teach the player how to think like a detective.

**Bad Note:** `"The IP address is 192.168.1.55."`

**Good (Luc) Note:** `"A local IP address in a secure server log? That’s sloppy. Someone was in the building, bypassing the firewall entirely. I need to check physical access logs, not just network traffic."`

## 5. Six Rules for Authors

1.  **No Sci-Fi Tech:** Technology should be realistic (Unix commands, logs, IP addresses). No "Enhance" buttons or magic tricks.
2.  **The Story is Noir:** The world is rainy, dirty, and full of human error.
3.  **Educational Value:** The player should leave knowing something new (e.g., how a port works or how timestamps work).
4.  **No Teleport:** If Luc goes from A to B, there must be a record of it (gas receipt, note about traffic).
5.  **Clear Resolution:** Each puzzle must end with a clear outcome that moves the story forward (Name, Place, Time).
6.  **Lore is Everywhere:** Use Lyon Herald articles, blog posts, and forum threads to deepen the world.

---
## 📋 Case Template (Copy/Paste)
Below is a template you should use when writing a new case.

```markdown
# CASE TITLE: [Case Name]
# AUTHOR: [Author Name]
# DIFFICULTY: [Easy / Medium / Hard]

---

## 📨 1. BRIEFING (Claire & Luc)
**Context:** Why are we here? Who is the client?
**Claire (Email/Msg):** "[Corporate speak introduction to the problem]"
**Luc (Personal Note):** "[Sarcastic translation of what Claire said + travel plan]"

---

## 📍 2. LEAD 01: [Location Name, e.g., The Old Bank]
**Location Vibe:** [Short description of the location for designers/players]

**📂 FILES ON DESK:**
1.  **Flavor (Lore):** [File name + Description of content]
2.  **Hard Evidence (Puzzle):** [File name + How the puzzle works]
3.  **Soft Evidence (Witness):** [File name + What does the witness say?]

**🗝️ FINDING LOGIC:**
* **Input:** [What data does the player use?]
* **Output:** [What does he find? e.g., License plate]
* **The Bridge (What connects to the next lead?):** [E.g., An address found in the shipping manifest points to the warehouse.]

---

## 📍 3. LEAD 02: [Location Name, e.g., The Garage]
**Luc's Travel Log:** "[Short text about the journey from Lead 01]"

**📂 FILES ON DESK:**
1.  **Flavor (Lore):** ...
2.  **Hard Evidence (Puzzle):** ...
3.  **Soft Evidence (Witness):** ...

**🗝️ FINDING LOGIC:**
* **Input:** ...
* **Output:** ...
* **The Bridge (What connects to the next lead?):** [E.g., An address found in the shipping manifest points to the warehouse.]

---

## 🏁 4. CONCLUSION (Final Destination)
**Luc's Final Report:** "[How did the case end?]"
**Claire's Feedback:** "[Was she happy with 'KPIs'?]"
```