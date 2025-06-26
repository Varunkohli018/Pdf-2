// script.js

function navigateTo(sectionId) { document.querySelectorAll('main, section').forEach(s => s.classList.add('hidden')); document.getElementById(sectionId + 'Page').classList.remove('hidden'); }

function goHome() { document.querySelectorAll('main, section').forEach(s => s.classList.add('hidden')); document.getElementById('homePage').classList.remove('hidden'); }

// TEXT TO PDF async function createTextPdf() { const { jsPDF } = window.jspdf; const text = document.getElementById("pdfText").value; const doc = new jsPDF(); doc.text(text || "No content entered.", 10, 20); const blob = doc.output('blob'); saveFile("text_to_pdf.pdf", blob); }

// IMAGE TO PDF function handleImageInput(source) { const input = document.getElementById("imageInput"); input.accept = "image/*"; input.capture = source === 'camera' ? 'environment' : ''; input.click(); }

async function createImagePdf() { const { jsPDF } = window.jspdf; const input = document.getElementById("imageInput"); const files = input.files; const doc = new jsPDF();

if (!files || files.length === 0) { alert("Please select image(s)."); return; }

for (let i = 0; i < files.length; i++) { const img = await toBase64(files[i]); doc.addImage(img, 'JPEG', 10, 10, 180, 160); if (i < files.length - 1) doc.addPage(); }

const blob = doc.output('blob'); saveFile("image_to_pdf.pdf", blob); }

function toBase64(file) { return new Promise((resolve, reject) => { const reader = new FileReader(); reader.readAsDataURL(file); reader.onload = () => resolve(reader.result); reader.onerror = error => reject(error); }); }

// MERGE PDFs using PDF-lib async function mergeFiles() { const input = document.getElementById("mergeInput"); const files = input.files; if (!files.length) return alert("Select PDF files to merge.");

const mergedPdf = await PDFLib.PDFDocument.create();

for (const file of files) { const arrayBuffer = await file.arrayBuffer(); const pdf = await PDFLib.PDFDocument.load(arrayBuffer); const copiedPages = await mergedPdf.copyPages(pdf, pdf.getPageIndices()); copiedPages.forEach(p => mergedPdf.addPage(p)); }

const mergedBytes = await mergedPdf.save(); const blob = new Blob([mergedBytes], { type: "application/pdf" }); saveFile("merged.pdf", blob); }

// EDIT PDF function editPdf() { const { jsPDF } = window.jspdf; const text = document.getElementById("editText").value; const doc = new jsPDF(); doc.text(text || "No edits made.", 10, 20); const blob = doc.output('blob'); saveFile("edited.pdf", blob); }

// RECEIPT PDF GENERATOR function createReceiptPdf() { const { jsPDF } = window.jspdf; const date = document.getElementById("r_date").value; const name = document.getElementById("r_name").value; const item = document.getElementById("r_item").value; const qty = document.getElementById("r_qty").value; const price = document.getElementById("r_price").value;

const total = qty * price;

const doc = new jsPDF(); doc.setFontSize(16); doc.text("Receipt", 90, 20); doc.setFontSize(12); doc.text(Date: ${date}, 20, 40); doc.text(Customer: ${name}, 20, 50); doc.text(Item: ${item}, 20, 60); doc.text(Quantity: ${qty}, 20, 70); doc.text(Price per Item: ₹${price}, 20, 80); doc.text(Total: ₹${total}, 20, 90);

const blob = doc.output('blob'); saveFile("receipt.pdf", blob); }

// SAVE FILE + LIST IN LOCALSTORAGE function saveFile(name, blob) { const reader = new FileReader(); reader.onloadend = () => { const base64 = reader.result; const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); files.push({ name, data: base64 }); localStorage.setItem("pdf_files", JSON.stringify(files)); const link = document.createElement("a"); link.href = base64; link.download = name; link.click(); loadMyFiles(); }; reader.readAsDataURL(blob); }

function loadMyFiles() { const list = document.getElementById("fileList"); list.innerHTML = ""; const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); if (!files.length) { list.innerHTML = "<li>No files found.</li>"; return; } files.forEach((file, index) => { const li = document.createElement("li"); li.innerHTML = <span>${file.name}</span> <div> <button onclick="openFile(${index})">Open</button> <button onclick="shareFile(${index})">Share</button> <button onclick="deleteFile(${index})">Delete</button> </div>; list.appendChild(li); }); }

function openFile(index) { const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); const file = files[index]; const win = window.open(); win.document.write(<iframe width='100%' height='100%' src='${file.data}'></iframe>); }

function shareFile(index) { const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); const file = files[index]; fetch(file.data) .then(res => res.blob()) .then(blob => { const fileToShare = new File([blob], file.name, { type: "application/pdf" }); if (navigator.canShare && navigator.canShare({ files: [fileToShare] })) { navigator.share({ title: file.name, files: [fileToShare] }); } else { alert("Sharing not supported on this device."); } }); }

function deleteFile(index) { const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); files.splice(index, 1); localStorage.setItem("pdf_files", JSON.stringify(files)); loadMyFiles(); }

window.onload = () => { document.getElementById("cameraBtn").onclick = () => handleImageInput('camera'); document.getElementById("galleryBtn").onclick = () => handleImageInput('gallery'); document.getElementById("fileBtn").onclick = () => { const input = document.getElementById("imageInput"); input.accept = "image/*,.pdf,.doc,.docx"; input.capture = ''; input.click(); }; loadMyFiles(); };

// script.js

function navigateTo(sectionId) { document.querySelectorAll('main, section').forEach(s => s.classList.add('hidden')); document.getElementById(sectionId + 'Page').classList.remove('hidden'); }

function goHome() { document.querySelectorAll('main, section').forEach(s => s.classList.add('hidden')); document.getElementById('homePage').classList.remove('hidden'); }

// TEXT TO PDF async function createTextPdf() { const { jsPDF } = window.jspdf; const text = document.getElementById("pdfText").value; const doc = new jsPDF(); doc.text(text || "No content entered.", 10, 20); const blob = doc.output('blob'); saveFile("text_to_pdf.pdf", blob); }

// IMAGE TO PDF function handleImageInput(source) { const input = document.getElementById("imageInput"); input.accept = "image/*"; input.capture = source === 'camera' ? 'environment' : ''; input.click(); }

async function createImagePdf() { const { jsPDF } = window.jspdf; const input = document.getElementById("imageInput"); const files = input.files; const doc = new jsPDF();

if (!files || files.length === 0) { alert("Please select image(s)."); return; }

for (let i = 0; i < files.length; i++) { const img = await toBase64(files[i]); doc.addImage(img, 'JPEG', 10, 10, 180, 160); if (i < files.length - 1) doc.addPage(); }

const blob = doc.output('blob'); saveFile("image_to_pdf.pdf", blob); }

function toBase64(file) { return new Promise((resolve, reject) => { const reader = new FileReader(); reader.readAsDataURL(file); reader.onload = () => resolve(reader.result); reader.onerror = error => reject(error); }); }

// MERGE PDFs using PDF-lib async function mergeFiles() { const input = document.getElementById("mergeInput"); const files = input.files; if (!files.length) return alert("Select PDF files to merge.");

const mergedPdf = await PDFLib.PDFDocument.create();

for (const file of files) { const arrayBuffer = await file.arrayBuffer(); const pdf = await PDFLib.PDFDocument.load(arrayBuffer); const copiedPages = await mergedPdf.copyPages(pdf, pdf.getPageIndices()); copiedPages.forEach(p => mergedPdf.addPage(p)); }

const mergedBytes = await mergedPdf.save(); const blob = new Blob([mergedBytes], { type: "application/pdf" }); saveFile("merged.pdf", blob); }

// EDIT PDF function editPdf() { const { jsPDF } = window.jspdf; const text = document.getElementById("editText").value; const doc = new jsPDF(); doc.text(text || "No edits made.", 10, 20); const blob = doc.output('blob'); saveFile("edited.pdf", blob); }

// RECEIPT PDF GENERATOR function createReceiptPdf() { const { jsPDF } = window.jspdf; const date = document.getElementById("r_date").value; const name = document.getElementById("r_name").value; const item = document.getElementById("r_item").value; const qty = document.getElementById("r_qty").value; const price = document.getElementById("r_price").value;

const total = qty * price;

const doc = new jsPDF(); doc.setFontSize(16); doc.text("Receipt", 90, 20); doc.setFontSize(12); doc.text(Date: ${date}, 20, 40); doc.text(Customer: ${name}, 20, 50); doc.text(Item: ${item}, 20, 60); doc.text(Quantity: ${qty}, 20, 70); doc.text(Price per Item: ₹${price}, 20, 80); doc.text(Total: ₹${total}, 20, 90);

const blob = doc.output('blob'); saveFile("receipt.pdf", blob); }

// SAVE FILE + LIST IN LOCALSTORAGE function saveFile(name, blob) { const reader = new FileReader(); reader.onloadend = () => { const base64 = reader.result; const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); files.push({ name, data: base64 }); localStorage.setItem("pdf_files", JSON.stringify(files)); const link = document.createElement("a"); link.href = base64; link.download = name; link.click(); loadMyFiles(); }; reader.readAsDataURL(blob); }

function loadMyFiles() { const list = document.getElementById("fileList"); list.innerHTML = ""; const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); if (!files.length) { list.innerHTML = "<li>No files found.</li>"; return; } files.forEach((file, index) => { const li = document.createElement("li"); li.innerHTML = <span>${file.name}</span> <div> <button onclick="openFile(${index})">Open</button> <button onclick="shareFile(${index})">Share</button> <button onclick="deleteFile(${index})">Delete</button> </div>; list.appendChild(li); }); }

function openFile(index) { const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); const file = files[index]; const win = window.open(); win.document.write(<iframe width='100%' height='100%' src='${file.data}'></iframe>); }

function shareFile(index) { const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); const file = files[index]; fetch(file.data) .then(res => res.blob()) .then(blob => { const fileToShare = new File([blob], file.name, { type: "application/pdf" }); if (navigator.canShare && navigator.canShare({ files: [fileToShare] })) { navigator.share({ title: file.name, files: [fileToShare] }); } else { alert("Sharing not supported on this device."); } }); }

function deleteFile(index) { const files = JSON.parse(localStorage.getItem("pdf_files") || "[]"); files.splice(index, 1); localStorage.setItem("pdf_files", JSON.stringify(files)); loadMyFiles(); }

window.onload = () => { document.getElementById("cameraBtn").onclick = () => handleImageInput('camera'); document.getElementById("galleryBtn").onclick = () => handleImageInput('gallery'); document.getElementById("fileBtn").onclick = () => { const input = document.getElementById("imageInput"); input.accept = "image/*,.pdf,.doc,.docx"; input.capture = ''; input.click(); }; loadMyFiles(); };

