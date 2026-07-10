// Initialize the Miro SDK
miro.onReady(() => {
  document.getElementById('start-btn').addEventListener('click', () => logTime('START'));
  document.getElementById('end-btn').addEventListener('click', () => logTime('END'));
});

async function logTime(type) {
  try {
    // 1. Get current user and time
    const userInfo = await miro.board.getUserInfo();
    const timestamp = new Date().toLocaleString();
    
    // 2. Get the center of the current view to drop the note
    const viewport = await miro.board.viewport.get();
    const x = viewport.x + viewport.width / 2;
    const y = viewport.y + viewport.height / 2;

    // 3. Create the sticky note with the data
    const sticky = await miro.board.createStickyNote({
      content: `<strong>${type} TIME</strong><br>User: ${userInfo.id}<br>Time: ${timestamp}`,
      x: x,
      y: y,
      style: {
        fillColor: type === 'START' ? 'light_green' : 'light_pink'
      }
    });

    // 4. LOCK IT IMMEDIATELY
    // This prevents accidental editing, though board owners can still unlock it.
    await miro.board.utils.lock(sticky.id);
    
    // Optional: Send this data to your own database/Google Sheet here for 100% tamper-proof logs
    
    alert(`${type} time recorded and locked!`);
  } catch (error) {
    console.error("Error creating timestamp:", error);
  }
}
