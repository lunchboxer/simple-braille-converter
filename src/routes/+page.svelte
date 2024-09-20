<script>
    let inputText = "";
    let brailleOutput = "";
    let mirroredOutput = "";

    const brailleMap = {
        ",": "1",
        ";": "2",
        ":": "3",
        ".": "4",
        "!": "6",
        "(": "7",
        ")": "7",
        "?": "8",
        '"': "8",
        "'": "9",
        "[": ",7",
        "]": "7,",
        "*": "99",
        _: "--",
        "...": "'''",
        "%": "@3p",
    };

    function convertToBraille(text) {
        return text
            .split("")
            .map((char) => {
                if (/[A-Z]/.test(char)) {
                    return `,${char.toLowerCase()}`;
                } else if (/[0-9]/.test(char)) {
                    return `#${char}`;
                } else if (char in brailleMap) {
                    return brailleMap[char];
                } else {
                    return char;
                }
            })
            .join("");
    }

    // need to reverse capital marker and all that punctation too.
    function mirrorString(text) {
        const mirrorMap = {
            a: "@",
            "`": "a",
            "@": "a",
            b: "^",
            "^": "b",
            c: "c",
            d: "f",
            e: "i",
            f: "d",
            g: "g",
            h: "j",
            i: "e",
            j: "h",
            k: ".",
            ".": "k",
            l: "_",
            _: "l",
            m: "%",
            "%": "m",
            n: "$",
            $: "n",
            o: "[",
            "[": "o",
            p: "?",
            "?": "p",
            q: "}",
            "}": "q",
            "]": "q",
            r: "w",
            s: ":",
            ":": "s",
            t: "\\",
            "\\": "t",
            u: "+",
            "+": "u",
            v: "#",
            "#": "v",
            w: "r",
            x: "x",
            y: "&",
            "&": "y",
            z: "!",
            "!": "z",
            "'": ",",
            ",": "'",
            "1": '"',
            '"': "1",
            "2": ";",
            ";": "2",
            "3": "3",
            "4": "6",
            "5": "9",
            "9": "5",
            "7": "7",
            "8": "0",
            "(": ")",
            ")": "(",
            "*": "/",
            "/": "*",
            "<": ">",
            ">": "<",
        };

        return text
            .split("")
            .map((char) => mirrorMap[char] || char)
            .reverse()
            .join("");
    }

    $: {
        brailleOutput = convertToBraille(inputText);
        mirroredOutput = mirrorString(brailleOutput);
    }
</script>

<main>
    <h1>Braille Converter</h1>
    <p>Might not yet accurately represent all punctuation.</p>
    <input bind:value={inputText} placeholder="Enter text here" />

    <div class="output">
        <h2>Braille:</h2>
        <p style="font-family: 'SimBraille', sans-serif;">{brailleOutput}</p>
    </div>

    <div class="output">
        <h2>Mirrored Braille:</h2>
        <p style="font-family: 'SimBraille', sans-serif;">{mirroredOutput}</p>
    </div>
</main>

<style>
    @font-face {
        font-family: "SimBraille";
        src: url("path/to/SimBraille.ttf") format("truetype");
    }

    main {
        font-family: Arial, sans-serif;
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
    }

    input {
        width: 100%;
        padding: 10px;
        margin-bottom: 20px;
        font-size: 16px;
    }

    .output {
        margin-bottom: 20px;
    }

    h2 {
        margin-bottom: 5px;
    }

    p {
        font-size: 24px;
        word-wrap: break-word;
    }
</style>
