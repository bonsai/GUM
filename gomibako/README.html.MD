<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>IME Persona Patch</title>
  </head>
  <body>
    <header>
      <h1>IME Persona Patch</h1>
      <p>Personalized input, without changing your IME.</p>
      <p>
        IME learns who you are, without ever seeing what you type.
      </p>
    </header>

    <section>
      <h2>What is this?</h2>
      <p>
        IME Persona Patch is an experimental system that adds a personalization layer on top of existing IMEs
        (Google Japanese Input / Mozc, etc.), without modifying them.
      </p>
      <p>It does not try to replace your IME. It quietly augments it.</p>
      <ul>
        <li>No new keyboard</li>
        <li>No OS-level replacement</li>
        <li>No cloud dependency required</li>
      </ul>
      <p>
        Just a thin, local “persona patch” between your thoughts and your input.
      </p>
    </section>

    <section>
      <h2>Motivation</h2>
      <p>Modern IMEs are extremely good at:</p>
      <ul>
        <li>general language correctness</li>
        <li>new words and trends</li>
        <li>average user behavior</li>
      </ul>
      <p>But they are still very bad at:</p>
      <ul>
        <li>your metaphors</li>
        <li>your recurring explanations</li>
        <li>your way of hesitating, rephrasing, or simplifying</li>
        <li>long-term personal context</li>
      </ul>
      <p>Meanwhile:</p>
      <ul>
        <li>LLMs remember context</li>
        <li>RAG remembers knowledge</li>
        <li>IME still forgets you</li>
      </ul>
      <p>
        This project explores a simple question: What if an IME could have a personality,
        without becoming intrusive or surveillance-based?
      </p>
    </section>

    <section>
      <h2>Core Idea</h2>
      <p>Instead of training a new IME from scratch, we:</p>
      <ul>
        <li>Observe how you revise, rephrase, and reuse expressions</li>
        <li>Distill only the high-confidence “surface layer” of your thinking</li>
        <li>Promote that layer into your IME user dictionary</li>
        <li>Do it locally, quietly, and reversibly</li>
      </ul>
      <p>Think of it as:</p>
      <ul>
        <li>RAG → skimming → IME</li>
        <li>knowledge → expression → habit</li>
      </ul>
    </section>

    <section>
      <h2>What this is not</h2>
      <ul>
        <li>❌ Not a replacement IME</li>
        <li>❌ Not a cloud learning system</li>
        <li>❌ Not a keystroke logger</li>
        <li>❌ Not an auto-completion spammer</li>
      </ul>
      <p>This project explicitly avoids:</p>
      <ul>
        <li>full text storage</li>
        <li>aggressive prediction</li>
        <li>UI noise</li>
        <li>model retraining at the IME level</li>
      </ul>
    </section>

    <section>
      <h2>Architecture (High Level)</h2>
      <pre>
Speech / Text / Edits
        ↓
   Python Core
 (RAG + embeddings)
        ↓
   Go Filter
 (skimming & decay)
        ↓
  Java IME Bridge
 (user dictionary sync)
        ↓
 Existing IME
      </pre>
    </section>

    <section>
      <h2>Language Roles</h2>
      <dl>
        <dt>Python</dt>
        <dd>RAG, embeddings, expression extraction, bias modeling</dd>
        <dt>Go</dt>
        <dd>Fast filtering, time decay, promotion thresholds</dd>
        <dt>Java</dt>
        <dd>User dictionary integration (Mozc / Google IME / Android IME)</dd>
        <dt>TypeScript</dt>
        <dd>UI for visibility, control, and demos</dd>
      </dl>
    </section>

    <section>
      <h2>What gets promoted to the IME?</h2>
      <p>Not raw words. Only expressions that are:</p>
      <ul>
        <li>reused over time</li>
        <li>stable (not frequently edited)</li>
        <li>short, expressive, and reusable</li>
        <li>clearly “you”</li>
      </ul>
      <p>Examples:</p>
      <ul>
        <li>definitions you keep explaining the same way</li>
        <li>metaphors you naturally reuse</li>
        <li>sentence starters you trust</li>
      </ul>
    </section>

    <section>
      <h2>Speech Recognition (Optional)</h2>
      <p>Speech recognition is treated as input hypotheses, not truth.</p>
      <ul>
        <li>Generic ASR (Google / Whisper) → 70% accuracy is enough</li>
        <li>Personal bias is applied after recognition</li>
        <li>Corrections are learning signals</li>
        <li>Silence and hesitation are signals too</li>
      </ul>
      <p>We optimize how it misunderstands you, not raw accuracy.</p>
    </section>

    <section>
      <h2>Privacy &amp; Philosophy</h2>
      <ul>
        <li>Local-first by default</li>
        <li>No mandatory cloud sync</li>
        <li>No behavioral scoring</li>
        <li>No “learning notifications”</li>
      </ul>
      <p>Learning should feel invisible.</p>
      <p>If the system makes you self-conscious, it’s broken.</p>
    </section>

    <section>
      <h2>Why a “Patch”?</h2>
      <p>
        IME is one of the most latency-sensitive, platform-dependent components in computing.
      </p>
      <p>Replacing it is unrealistic. Extending it is respectful.</p>
      <p>This project treats IME as:</p>
      <p>a sacred final layer that should be enhanced, not disrupted.</p>
    </section>

    <section>
      <h2>Status</h2>
      <p>🚧 Experimental / Research-grade</p>
      <p>Currently focused on:</p>
      <ul>
        <li>personal RAG distillation</li>
        <li>dictionary promotion heuristics</li>
        <li>Mozc / Google IME user dictionary workflows</li>
      </ul>
    </section>

    <section>
      <h2>Who is this for?</h2>
      <ul>
        <li>Developers with strong personal writing habits</li>
        <li>Researchers exploring personalization without surveillance</li>
        <li>IME / HCI / NLP engineers</li>
        <li>Anyone who feels their tools are smart, but not familiar</li>
      </ul>
    </section>

    <section>
      <h2>License</h2>
      <p>TBD (likely Apache-2.0 or MIT)</p>
    </section>

    <section>
      <h2>One-line Summary</h2>
      <p>
        IME Persona Patch explores how input methods can adapt to individuals
        without retraining models, replacing keyboards, or sending data to the cloud.
      </p>
    </section>
  </body>
</html>
