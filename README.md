# Online Voting System with Facial Recognition

This repository contains a Flask-based web application that implements a secure online voting system using facial recognition for user authentication. The system ensures that only registered users whose faces match their profiles can cast a vote, preventing fraudulent voting activities.

## Features

* **User Registration:** Users can sign up by providing their details and capturing their facial data via webcam.


* **Dual Authentication:** Users log in with a username and password, followed by a facial validation step comparing their live capture to the registered image.


* **Secure Voting Mechanism:** Only authenticated and verified users are granted access to the voting page.


* **Double-Vote Prevention:** The system checks if a user's email has already cast a vote, preventing multiple submissions from the same user.


* **Real-time Results:** Tallying functionality to view vote counts, a list of voters, and the overall winner.



---

## Technologies Used

* **Backend:** Python with the Flask web framework.


* **Database:** SQLite3 for managing user profiles, face data references, and vote records.


* **Facial Recognition:** The `face_recognition` and `cv2` Python libraries handle backend image encoding and comparisons.


* **Frontend:** HTML, CSS, and JavaScript utilizing Axios for HTTP requests and device APIs for webcam access.


* **Client-Side ML:** Uses TensorFlow.js and `face-api.js` for client-side face detection functionalities.



---

## Database Structure

The application uses an SQLite database (`data.db`) containing three primary tables:

* **`register`**: Stores user account credentials.
* Fields: `id` (Primary Key), `first`, `last`, `email` (Unique), `password`, `con_password`.




* **`faceData`**: Links user emails to their specific face image timestamp ID.
* Fields: `id` (Primary Key), `email` (Unique), `face_id` (Unique).




* **`vote`**: Records the votes cast by users.
* Fields: `id` (Primary Key), `email` (Unique), `user_vote`.





---

## Setup & Installation

### Prerequisites

* Python 3.x
* A C++ compiler (often required to build the `dlib` dependency for `face_recognition`).

### Installation Steps

1. **Clone the repository and install dependencies:**
Ensure you install Flask, OpenCV (`cv2`), `face_recognition`, and `sqlite3` (usually included in standard Python).


```bash

```



pip install Flask opencv-python face_recognition

```
2.  **Database Initialization:**
    Run the setup script to initialize `data.db` and the required tables[cite: 3].
    ```python
    import sqlite3
    db = sqlite3.connect("data.db")
    cursor = db.cursor()
    cursor.execute('''CREATE TABLE IF NOT EXISTS faceData (id INTEGER PRIMARY KEY AUTOINCREMENT, email TEXT UNIQUE NOT NULL, face_id INTERGER UNIQUE NOT NULL)''')
    db.commit()
    db.close()

```

3. **Prepare Directory:**
Ensure there is a directory named `Face_img` in your project root, as the application relies on it to save captured images.


4. **Run the App:**
Start the Flask server.


```bash
python app.py

```



```

---

## Usage Workflow

1.  **Registration:** Navigate to the `/register` route to create an account[cite: 1]. The system will prompt for webcam access to capture and link your face data[cite: 7].
2.  **Login:** Go to the home route (`/`) and log in using your registered credentials[cite: 1, 6].
3.  **Validation:** Upon entering valid credentials, you are redirected to `/valid_face`, where the webcam will capture a live image and compare it to your registered profile[cite: 1, 10].
4.  **Voting:** If the server returns "Faces match," you proceed to the `/vote` page to select your candidate[cite: 1, 10].
5.  **Results:** You can view the list of voters at `/voted_list` or see the final counts and winner at `/vote_result`[cite: 1].

```
