# console_static_text

Zero dependency crate for logging text that should stay in the same place in a console. This measures words to handle wrapping and has some console resizing support. For an example, this could be used for displaying progress bars or inputs.

Example use with the [console](https://crates.io/crates/console) crate:

```rs
use console_static_text::ConsoleStaticText;
use console_static_text::ConsoleStaticTextOptions;

let mut static_text = ConsoleStaticText::new(
  ConsoleStaticTextOptions {
    // I honestly haven't tested this
    strip_ansi_codes: Box::new(console::strip_ansi_codes),
    terminal_width: Box::new(|| console::Term::stderr().size().1),
  },
);

static_text.eprint("initial\ntext");
// will clear the previous text and put this new text
static_text.eprint("new text");

// or get the text manually
if let Some(text) = static_text.get_update_text("new text") {
  eprint!("{}", text);
}

// clear out the previous text
static_text.eprint_clear();
```