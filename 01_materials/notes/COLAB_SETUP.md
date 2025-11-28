# Using Google Colab with GitHub for GPU Acceleration

Google Colab gives you free access to powerful NVIDIA GPUs directly through your browser.  
This guide explains how to open your notebooks from GitHub, enable GPU hardware, and save your work properly.

---

## 1. Access Google Colab

1. Go to **[https://colab.research.google.com](https://colab.research.google.com)**  
2. Sign in with your Google account.  
3. In the dialog that appears, select the **GitHub** tab.

---

## 2. Open a Notebook from GitHub

1. Paste your repository URL, for example:
   ```
   https://github.com/<username>/<repo>
   ```
2. Press **Enter** to search.
3. Click the notebook (`.ipynb`) you want to open.  
   Colab loads the latest version directly from GitHub.

### Direct Link Pattern
You can open any notebook instantly with a link like:
```
https://colab.research.google.com/github/<username>/<repo>/blob/main/<notebook>.ipynb
```
Example:
```
https://colab.research.google.com/github/andrewharris/deep-learning-notes/blob/main/lab6.ipynb
```

---

## 3. Enable GPU Acceleration

1. In Colab, go to the top menu:  
   **Runtime → Change runtime type**
2. Under **Hardware accelerator**, choose **GPU**, then click **Save.**
3. Verify the GPU is active:

   ```python
   import torch
   print("CUDA available:", torch.cuda.is_available())
   !nvidia-smi
   ```

   You should see information for a Tesla T4, P100, or A100 GPU.

---

## 4. Install Required Packages

Each Colab session starts fresh, so install dependencies in the first code cell:

```python
!pip install torch torchvision matplotlib scikit-learn tqdm
```

Add any other libraries your notebook needs.

---

## 5. Save and Load Data from Google Drive (Optional)

If your notebook reads or saves large files, mount Drive:

```python
from google.colab import drive
drive.mount('/content/drive')
```

Your Drive appears at `/content/drive/MyDrive/`.  
Example:
```python
model_path = "/content/drive/MyDrive/models/model.pt"
torch.save(model.state_dict(), model_path)
```

---

## 6. Save Changes Back to GitHub

When you finish editing:

- **File → Save a copy in GitHub**  
- Choose your repo and branch (e.g., `main`)  
- Add a short commit message → **OK**

Now your GPU-executed notebook is version-controlled in GitHub.

---

## 7. Synchronize with Local VS Code or Jupyter

If you also keep a local copy:

```bash
git pull origin main
```
That updates your local notebook to include edits made in Colab.

---

## 8. Common Issues & Fixes

| Problem | Cause | Fix |
|----------|--------|-----|
| `torch.cuda.is_available()` → False | GPU not enabled | Runtime → Change runtime type → GPU |
| “NVIDIA-SMI has failed” | GPU pool busy | Factory Reset Runtime, then re-enable GPU |
| Files disappear after reconnect | Colab sessions are temporary | Mount Drive and save files there |
| Packages missing after restart | New runtime | Re-run `!pip install …` cells |
| Quota exceeded | Too much GPU usage | Wait a few hours or use Colab Pro |

---

## 9. Why Use Colab for Deep Learning?

| Benefit | Description |
|----------|-------------|
| **Speed** | GPUs train models 10-100× faster than CPUs. |
| **Cost Efficiency** | Free tier includes GPUs; Pro tiers add reliability. |
| **Accessibility** | Works from any computer with a browser. |
| **Reproducibility** | Everyone in the class can use identical hardware. |
| **Integration** | One click from GitHub → GPU runtime → save back to GitHub. |

---

## 10. Quick Start Checklist

| Step | Action |
|------|--------|
| 1 | Go to [Colab](https://colab.research.google.com) |
| 2 | Open your GitHub notebook |
| 3 | Enable GPU |
| 4 | Install dependencies |
| 5 | Mount Drive (optional) |
| 6 | Run training or analysis |
| 7 | Save copy to GitHub |

---

## Badge for Your Repository

Add this Markdown snippet to the top of your notebook or README so classmates can open it instantly:

```markdown
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](
https://colab.research.google.com/github/<username>/<repo>/blob/main/<notebook>.ipynb)
```

---

### Summary

Google Colab provides a straightforward way to leverage GPU acceleration without buying hardware.  
By linking it with GitHub, you gain free compute power **and** version control — an ideal setup for collaborative deep-learning coursework.
