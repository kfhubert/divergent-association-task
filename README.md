# Divergent Association Task code

The DAT measures creativity in under 4 minutes. It involves thinking of 10
unrelated words. Creative people choose words with greater semantic distances
between them.

See our [preprint](https://psyarxiv.com/qvg8b/) for more details.

## Online version

Try the task and see your score at
[datcreativity.com](https://www.datcreativity.com).

## Installation

1. Clone this code:

    - `git clone https://github.com/jayolson/divergent-association-task.git`

2. Install [Python 3](https://www.python.org) and [pip](https://pypi.org/project/pip/).

3. Download the dependencies and model:

    - `make install` on Unix-like systems

    - or else:

        - `pip3 install --user numpy scipy`

        - Download and extract glove.840B.300d.zip from <https://nlp.stanford.edu/projects/glove/>

4. Try it:

    - `python3 examples.py`

## Examples

See examples.py:

    import dat

    # GloVe model from https://nlp.stanford.edu/projects/glove/
    model = dat.Model("glove.840B.300d.txt", "words.txt")

    # Compound words are translated into words found in the model
    model.validate("cul de sac") # cul-de-sac

    # Compute the cosine distance between 2 words (0 to 2)
    model.distance("cat", "dog") # 0.1983
    model.distance("cat", "thimble") # 0.8787

    # Compute the DAT score between 2 words (average cosine distance * 100)
    model.dat(["cat", "dog"], 2) # 19.83
    model.dat(["cat", "thimble"], 2) # 87.87

    # Word examples (Figure 1 in paper)
    low = ["arm", "eyes", "feet", "hand", "head", "leg", "body"]
    average = ["bag", "bee", "burger", "feast", "office", "shoes", "tree"]
    high = ["hippo", "jumper", "machinery", "prickle", "tickets", "tomato", "violin"]

    # Compute the DAT score (transformed average cosine distance of first 7 valid words)
    model.dat(low) # 50
    model.dat(average) # 78
    model.dat(high) # 95

## Data

For open data (8,900 participants from 98 countries), see
<https://osf.io/kbeq6/>.

## Credits

By [Jay Olson](https://www.jayolson.org) at Harvard University.

The dictionary (words.txt) is based on [Hunspell](https://hunspell.github.io)
by László Németh.

## License

MIT