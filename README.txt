Screenshots in this folder are genuine captures of this project, taken with
Playwright and headless Chromium 141 using software (SwiftShader) WebGL.

Things to know when comparing them with your own browser:
- The sandbox had no network access, so Google Fonts (Space Grotesk, DM Sans)
  did not load. Text is rendered in the system fallback font and looks wider
  than it will on a normal connection.
- Software WebGL is slower than a real GPU; the scene is identical but
  animation smoothness will be better on real hardware.

01-desktop-hero.png            1440x900 initial state
02-winner-celebration.png      moments after LAYER becomes sole leader
03-desktop-scoreboard-full.png full page with scores and activity log
04-reset-confirmation.png      reset confirmation dialog
05-mobile-full.png             390px-wide phone layout (2x)
