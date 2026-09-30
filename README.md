# MoodTape

> What music fits how I feel today?

MoodTape is a mood-based music recommendation app. You write a short morning journal entry, MoodTape detects your current mood from the text, and recommends songs from different decades that fit how you feel right now.

Unlike traditional recommenders, MoodTape does **not** use your listening history, favorite artists, or favorite genres. Recommendations are based only on your current emotional state.

## Philosophy

Most music apps answer: *"What music is similar to what I usually listen to?"*

MoodTape answers: *"What music fits how I feel today?"*

Because recommendations span multiple decades and genres, MoodTape also helps you discover music outside your usual taste.

## How It Works (Version 0.1)

1. Write a short morning journal entry.
2. MoodTape analyzes the text with simple keyword-based rules.
3. It detects your main mood.
4. It picks songs from `data/songs.csv` that match the mood and the selected mode.
5. It shows one song per decade (1970s to 2020s) when possible.

### Supported moods

`happy`, `sad`, `calm`, `lonely`, `energetic`, `tired`, `anxious`, `romantic`, `hopeful`, `neutral`

### Recommendation modes

| Mode    | What it does |
|---------|--------------|
| Match   | Songs that closely match your current mood. |
| Shift   | Songs that gently move your mood in a more positive or energetic direction. |
| Explore | Unexpected songs from different genres, artists, and decades that still connect emotionally to your mood. |

### Example

Journal:

```
I feel a little lonely today, but I also feel peaceful and want to take things slowly.
```

Detected mood: `lonely` (multiple moods are planned for v0.2)

Recommendations (Match mode):

```
1970s -> song
1980s -> song
1990s -> song
2000s -> song
2010s -> song
2020s -> song
```

## Tech Stack

- Python 3.10+
- Streamlit (user interface)
- Pandas (song data handling)
- CSV file (music dataset)
- Rule-based mood detection (no machine learning in v0.1)
- Git and GitHub (version control)

## Project Structure

```
MoodTape/
├── README.md             # Project description (this file)
├── app.py                # Streamlit UI: input, buttons, display only
├── requirements.txt      # Python dependencies
├── .gitignore            # Files Git should ignore
├── data/
│   └── songs.csv         # Song dataset
├── src/
│   ├── mood_detector.py  # detect_mood(text) -> mood
│   └── recommender.py    # load songs, filter by mood/mode, pick by decade
└── tests/                # Unit tests
```

Mood detection and recommendation logic are kept separate from the UI, so each part can be tested and improved independently.

## Dataset Format

`data/songs.csv` uses these columns:

| Column | Description | Example |
|--------|-------------|---------|
| title  | Song title | Dreams |
| artist | Artist name | Fleetwood Mac |
| year   | Release year | 1977 |
| genre  | Music genre | rock |
| mood   | One of the supported moods | calm |
| energy | `low`, `medium`, or `high` | medium |

```csv
title,artist,year,genre,mood,energy
Dreams,Fleetwood Mac,1977,rock,calm,medium
No Surprises,Radiohead,1997,alternative,sad,low
```

The `mood` value must be one of the supported moods listed above.

## Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/MoodTape.git
cd MoodTape

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the app
streamlit run app.py
```

## Roadmap

- **v0.1** — Rule-based mood detection, CSV dataset, Match / Shift / Explore modes, one song per decade *(in progress)*
- **v0.2** — Multiple moods, recommendation scores, better decade algorithm
- **v0.3** — Daily mood history, mood trends over time, personal monthly soundtrack
- **v0.4** — NLP and sentiment analysis
- **v0.5** — Text embeddings for emotions, emotional features for songs, similarity-based matching
- **v1.0** — Spotify (or other music API) integration, automatic playlists, user accounts, ML-based recommendations

## License

MIT
