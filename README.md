import random
from collections import defaultdict
# Sample text data for training
corpus = """
Implementing a Markov chain text generator can be quite simple. The algorithm predicts the next word 
in a sentence based on previous words. It’s often used for text generation.
"""

# Tokenize the text data into words
def tokenize_text(text):
    words = text.lower().split()
    return words

# Build the Markov Chain model
def build_markov_chain(words, order=2):
    markov_chain = defaultdict(list)

    # Create word pairs based on the specified order
    for i in range(len(words) - order):
        key = tuple(words[i:i+order])  # Get the tuple of words based on the order
        next_word = words[i + order]
        markov_chain[key].append(next_word)

    return markov_chain

# Generate text using the Markov Chain model
def generate_text(chain, start_words, length=20):
    current_words = start_words
    generated_words = list(start_words)

    for _ in range(length):
        current_key = tuple(current_words[-2:])  # Get the last two words as the key
        next_words = chain.get(current_key)

        if not next_words:
            break

        next_word = random.choice(next_words)
        generated_words.append(next_word)
        current_words.append(next_word)

    return ' '.join(generated_words)

# Tokenize the corpus and build the model
words = tokenize_text(corpus)
markov_chain = build_markov_chain(words)

# Generate text starting with a given word pair
start_words = ["markov", "chain"]
generated_text = generate_text(markov_chain, start_words, length=20)
print("Generated Text:\n", generated_text)
