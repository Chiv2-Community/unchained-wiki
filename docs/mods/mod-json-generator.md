# mod.json Generator

Use this interactive form to generate a properly formatted `mod.json` file for your Chivalry 2 mod. Simply fill in the fields below and click "Generate mod.json" to create your configuration file.

<div class="mod-json-generator">
  <form id="modJsonForm">
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
          <input type="text" class="dep-repo" placeholder="Repository URL (e.g., https://github.com/Chiv2-Community/Unchained-Mods)">
          <input type="text" class="dep-version" placeholder="Version (e.g., 0.1.0)">
          <button type="button" class="remove-dep" style="display:none;">Remove</button>
        </div>
      </div>
      <button type="button" id="addDependency">Add Dependency</button>
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

.form-group input[type="text"],
.form-group textarea,
.form-group select {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ccc;
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
  background: #dc3545;
  color: white;
  border: none;
  padding: 0.5rem;
  border-radius: 4px;
  cursor: pointer;
}

#addDependency {
  background: #007bff;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
}

.generate-button {
  background: #28a745;
  color: white;
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
  background: #f8f9fa;
  border-radius: 4px;
}

#outputContainer pre {
  background: #fff;
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
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
  background: #007bff;
  color: white;
}

#downloadButton {
  background: #6c757d;
  color: white;
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
    const modName = document.getElementById('modName').value;
    const modDescription = document.getElementById('modDescription').value;
    const modType = document.getElementById('modType').value;
    const modAuthors = document.getElementById('modAuthors').value.split(',').map(author => author.trim());

    // Get tags
    const tags = Array.from(document.querySelectorAll('input[name="modTags"]:checked'))
      .map(checkbox => checkbox.value);

    // Get dependencies
    const dependencies = [];
    document.querySelectorAll('.dependency-row').forEach(row => {
      const repo = row.querySelector('.dep-repo').value.trim();
      const version = row.querySelector('.dep-version').value.trim();
      if (repo && version) {
        dependencies.push({ repo_url: repo, version: version });
      }
    });

    // Create mod.json object
    const modJson = {
      name: modName,
      description: modDescription,
      mod_type: modType,
      authors: modAuthors,
      dependencies: dependencies,
      tags: tags
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
