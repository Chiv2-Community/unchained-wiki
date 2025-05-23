# mod.json Generator

Use this interactive form to generate a properly formatted `mod.json` file for your Chivalry 2 mod. Simply fill in the fields below and click "Generate mod.json" to create your configuration file.

<div class="mod-json-generator">
  <form id="modJsonForm">
    <div class="form-group">
      <label for="repoUrl">Repository URL *</label>
      <input type="text" id="repoUrl" required placeholder="https://github.com/yourusername/your-mod-repo">
    </div>

    <div class="form-group">
      <label for="modName">Mod Name *</label>
      <input type="text" id="modName" required placeholder="Your Mod Name">
    </div>

    <div class="form-group">
      <label for="modDescription">Description *</label>
      <textarea id="modDescription" required placeholder="A short description of your mod"></textarea>
    </div>

    <div class="form-group">
      <label for="modType">Mod Type *</label>
      <select id="modType" required>
        <option value="Client">Client - Client-side only</option>
        <option value="Server">Server - Server-side only</option>
        <option value="Shared">Shared - Client and server components</option>
      </select>
    </div>

    <div class="form-group">
      <label for="modAuthors">Authors *</label>
      <input type="text" id="modAuthors" required placeholder="Your Name (comma-separated for multiple authors)">
    </div>

    <div class="form-group">
      <label for="homePage">Home Page (optional)</label>
      <input type="text" id="homePage" placeholder="https://yourdocsite.com">
    </div>

    <div class="form-group">
      <label for="imageUrl">Image URL (optional)</label>
      <input type="text" id="imageUrl" placeholder="https://example.com/mod-image.png">
    </div>

    <div class="form-group">
      <label>Tags</label>
      <div class="checkbox-group">
        <label><input type="checkbox" name="modTags" value="Mutator"> Mutator - Gameplay modifications</label>
        <label><input type="checkbox" name="modTags" value="Map"> Map - Levels/maps</label>
        <label><input type="checkbox" name="modTags" value="Cosmetic"> Cosmetic - Visual modifications</label>
        <label><input type="checkbox" name="modTags" value="Audio"> Audio - Sound/music</label>
        <label><input type="checkbox" name="modTags" value="Model"> Model - 3D models</label>
        <label><input type="checkbox" name="modTags" value="Weapon"> Weapon - Weapon mods</label>
        <label><input type="checkbox" name="modTags" value="Doodad"> Doodad - Game extensions</label>
        <label><input type="checkbox" name="modTags" value="Library"> Library - Frameworks/libraries</label>
      </div>
    </div>

    <div class="form-group">
      <label>Dependencies</label>
      <div id="dependenciesContainer">
        <div class="dependency-row">
          <input type="text" class="dep-repo" placeholder="Repository URL (e.g., https://github.com/Chiv2-Community/Unchained-Mods)" value="https://github.com/Chiv2-Community/Unchained-Mods">
          <input type="text" class="dep-version" placeholder="Version (e.g., 0.1.0)" value="0.1.0">
          <button type="button" class="remove-dep" style="display:none;">Remove</button>
        </div>
        <div class="dependency-row">
          <input type="text" class="dep-repo" placeholder="Repository URL (e.g., https://github.com/Chiv2-Community/Unchained-Mods)">
          <input type="text" class="dep-version" placeholder="Version (e.g., 0.1.0)">
          <button type="button" class="remove-dep" style="display:none;">Remove</button>
        </div>
      </div>
      <button type="button" id="addDependency">Add Dependency</button>
    </div>

    <div class="form-group">
      <label for="maps">Maps (comma-separated list)</label>
      <input type="text" id="maps" placeholder="Map1, Map2">
      <small>List of maps this mod provides (if any)</small>
    </div>

    <div class="form-group">
      <label>
        <input type="checkbox" id="actorMod">
        Actor Mod (Check if your mod affects actors)
      </label>
    </div>

    <button type="submit" class="generate-button">Generate mod.json</button>
  </form>

  <div id="outputContainer" style="display:none;">
    <h3>Generated mod.json</h3>
    <pre><code id="generatedJson"></code></pre>
    <button id="copyButton">Copy to Clipboard</button>
    <button id="downloadButton">Download mod.json</button>
  </div>
</div>

<style>
.mod-json-generator {
  max-width: 800px;
  margin: 2rem auto;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.form-group small {
  display: block;
  margin-top: 0.25rem;
  color: var(--md-default-fg-color--light);
  font-size: 0.85rem;
}

.form-group input[type="text"],
.form-group textarea,
.form-group select {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid var(--md-default-fg-color--lightest);
  background-color: var(--md-default-bg-color);
  color: var(--md-default-fg-color);
  border-radius: 4px;
  font-size: 1rem;
}

.form-group textarea {
  min-height: 100px;
  resize: vertical;
}

.checkbox-group {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 0.5rem;
}

.checkbox-group label {
  display: flex;
  align-items: center;
  font-weight: normal;
}

.checkbox-group input[type="checkbox"] {
  margin-right: 0.5rem;
}

.dependency-row {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
}

.dep-repo {
  flex: 2;
}

.dep-version {
  flex: 1;
}

.remove-dep {
  background: var(--md-accent-fg-color);
  color: var(--md-accent-bg-color);
  border: none;
  padding: 0.5rem;
  border-radius: 4px;
  cursor: pointer;
}

#addDependency {
  background: var(--md-primary-fg-color);
  color: var(--md-primary-bg-color);
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
}

.generate-button {
  background: var(--md-primary-fg-color);
  color: var(--md-primary-bg-color);
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1.1rem;
  width: 100%;
}

#outputContainer {
  margin-top: 2rem;
  padding: 1rem;
  background: var(--md-code-bg-color);
  border: 1px solid var(--md-default-fg-color--lightest);
  border-radius: 4px;
}

#outputContainer pre {
  background: var(--md-code-bg-color);
  color: var(--md-code-fg-color);
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  margin: 0;
}

#outputContainer pre code {
  background: transparent;
  color: var(--md-code-fg-color);
  padding: 0;
}

#copyButton, #downloadButton {
  margin-right: 1rem;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

#copyButton {
  background: var(--md-primary-fg-color);
  color: var(--md-primary-bg-color);
}

#downloadButton {
  background: var(--md-default-fg-color--light);
  color: var(--md-default-bg-color);
}

/* Ensure buttons are visible on hover */
button:hover {
  opacity: 0.9;
}

/* Style for dark mode */
[data-md-color-scheme="slate"] {
  .form-group input[type="text"],
  .form-group textarea,
  .form-group select {
    border-color: var(--md-default-fg-color--lighter);
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const form = document.getElementById('modJsonForm');
  const outputContainer = document.getElementById('outputContainer');
  const generatedJson = document.getElementById('generatedJson');
  const copyButton = document.getElementById('copyButton');
  const downloadButton = document.getElementById('downloadButton');
  const addDependencyButton = document.getElementById('addDependency');
  const dependenciesContainer = document.getElementById('dependenciesContainer');

  // Add dependency row
  addDependencyButton.addEventListener('click', function() {
    const newRow = document.createElement('div');
    newRow.className = 'dependency-row';
    newRow.innerHTML = `
      <input type="text" class="dep-repo" placeholder="Repository URL">
      <input type="text" class="dep-version" placeholder="Version">
      <button type="button" class="remove-dep">Remove</button>
    `;
    dependenciesContainer.appendChild(newRow);
    updateRemoveButtons();
  });

  // Remove dependency row
  dependenciesContainer.addEventListener('click', function(e) {
    if (e.target.classList.contains('remove-dep')) {
      e.target.parentElement.remove();
      updateRemoveButtons();
    }
  });

  function updateRemoveButtons() {
    const rows = dependenciesContainer.querySelectorAll('.dependency-row');
    rows.forEach((row, index) => {
      const removeBtn = row.querySelector('.remove-dep');
      removeBtn.style.display = rows.length > 1 ? 'block' : 'none';
    });
  }

  // Form submission
  form.addEventListener('submit', function(e) {
    e.preventDefault();

    // Get form values
    const repoUrl = document.getElementById('repoUrl').value;
    const modName = document.getElementById('modName').value;
    const modDescription = document.getElementById('modDescription').value;
    const modType = document.getElementById('modType').value;
    const modAuthors = document.getElementById('modAuthors').value.split(',').map(author => author.trim());
    const homePage = document.getElementById('homePage').value || null;
    const imageUrl = document.getElementById('imageUrl').value || null;

    // Get tags
    const tags = Array.from(document.querySelectorAll('input[name="modTags"]:checked'))
      .map(checkbox => checkbox.value);

    // Get dependencies
    const dependencies = [ ];
    document.querySelectorAll('.dependency-row').forEach(row => {
      const repo = row.querySelector('.dep-repo').value.trim();
      const version = row.querySelector('.dep-version').value.trim();
      if (repo && version) {
        dependencies.push({ repo_url: repo, version: version });
      }
    });

    // Get maps and options
    const mapsInput = document.getElementById('maps').value.trim();
    const maps = mapsInput ? mapsInput.split(',').map(m => m.trim()).filter(m => m) : [];
    const actorMod = document.getElementById('actorMod').checked;

    // Create mod.json object
    const modJson = {
      repo_url: repoUrl,
      name: modName,
      description: modDescription,
      ...(homePage && { home_page: homePage }),
      ...(imageUrl && { image_url: imageUrl }),
      mod_type: modType,
      authors: modAuthors,
      dependencies: dependencies,
      tags: tags,
      maps: maps,
      options: {
        actor_mod: actorMod
      }
    };

    // Display the generated JSON
    generatedJson.textContent = JSON.stringify(modJson, null, 2);
    outputContainer.style.display = 'block';
    outputContainer.scrollIntoView({ behavior: 'smooth' });
  });

  // Copy to clipboard
  copyButton.addEventListener('click', function() {
    navigator.clipboard.writeText(generatedJson.textContent)
      .then(() => {
        copyButton.textContent = 'Copied!';
        setTimeout(() => {
          copyButton.textContent = 'Copy to Clipboard';
        }, 2000);
      })
      .catch(err => {
        console.error('Failed to copy:', err);
      });
  });

  // Download mod.json
  downloadButton.addEventListener('click', function() {
    const blob = new Blob([generatedJson.textContent], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'mod.json';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
  });
});
</script>
