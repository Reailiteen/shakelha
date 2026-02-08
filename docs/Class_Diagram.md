# classDiagram
    class User {
        id
        name
        isAI
        score
        rack
        missedTurns
        status
        playTurn()
        addScore()
        drawLetters()
        incrementMissedTurn()
        resetMissedTurns()
    }

    class Turn {
        turnNumber
        scoreGained
        isSkipped
        validateMove()
        calculateScore()
        commit()
    }

    class Timer {
        durationSeconds
        timeRemaining
        isExpired
        start()
        tick()
        expire()
        reset()
    }

    class Board {
        grid[11][11]
        multipliers[11][11]
        placeWord()
        isValidPlacement()
        getWordMultipliers()
    }

    class Word {
        text
        letters
        positions
        direction
        isValid()
        length()
        baseScore()
    }

    class Letter {
        char
        points
        rarity
        isBlank
        getScore()
    }

    class LetterBag {
        letters
        draw()
        shuffle()
        remainingCount()
    }

    User --> Turn
    Turn --> Board
    Turn --> Word
    Turn --> Timer
    Board --> Letter
    Word --> Letter
    Game --> LetterBag
    Game --> Board
    Game --> Users