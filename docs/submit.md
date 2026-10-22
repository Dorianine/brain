# 实验报告素材投递

!!! info "投递须知"
    本投递通道用于接收实验课件（PPT / PDF）及实验实拍图像（如微孔板显色、试纸条拍照等）。上传后素材将直接流式传输至本地后台，由 AI Agent 自动读取素材并完成符合杭师大规范的排版报告。

<div class="submit-card" markdown>

<form id="submissionForm" onsubmit="handleFormSubmit(event)">

<div class="form-grid">
  <div class="form-group">
    <label for="student_name">学生姓名 <span class="required">*</span></label>
    <input type="text" id="student_name" class="md-input" required placeholder="如：张三">
  </div>
  <div class="form-group">
    <label for="student_class">班级 / 学号</label>
    <input type="text" id="student_class" class="md-input" placeholder="如：护理25 / 3220xxxx">
  </div>
  <div class="form-group">
    <label for="experiment_name">实验项目 <span class="required">*</span></label>
    <input type="text" id="experiment_name" class="md-input" required value="免疫标记技术" placeholder="如：免疫标记技术">
  </div>
</div>

<div class="form-group">
  <label for="ppt_file">实验课件（PPT / PDF） <span class="required">*</span></label>
  <input type="file" id="ppt_file" class="file-input" accept=".pptx,.ppt,.pdf" required>
  <span class="field-hint">支持 .pptx, .ppt, .pdf 格式文件</span>
</div>

<div class="form-group">
  <label for="photo_files">实验实拍图像（支持多选） <span class="required">*</span></label>
  <input type="file" id="photo_files" class="file-input" accept="image/*" multiple required>
  <span class="field-hint">支持上传手机实拍微孔板显色、试纸条条带等照片</span>
</div>

<div class="form-group">
  <label for="notes">特殊要求与现象备注（选填）</label>
  <textarea id="notes" class="md-input" rows="3" placeholder="例如：老师强调讨论部分重点分析洗板误差；或记录特定孔位淡黄深浅等..."></textarea>
</div>

<div id="progressContainer" class="progress-container" style="display:none;">
  <div class="progress-labels">
    <span>正在传输数据流...</span>
    <span id="progressText">0%</span>
  </div>
  <div class="progress-track">
    <div id="progressBar" class="progress-bar"></div>
  </div>
</div>

<div id="statusAlert" class="status-alert" style="display:none;"></div>

<button type="submit" id="submitBtn" class="md-button md-button--primary submit-btn">
  提交素材数据流
</button>

</form>

</div>

??? note "传输节点配置"
    默认传输节点已配置为国内高速公网通道（`https://27c4615a.r8.cpolar.cn/api/upload`）。  
    无论访客在校园网、宿舍还是校外移动 5G 流量下，均可秒速直传到号主电脑。
    
    <input type="text" id="backendApiUrl" class="md-input" value="https://27c4615a.r8.cpolar.cn/api/upload" style="margin-top: 8px;">

<style>
/* 与 MkDocs Material 主题变量完全协同，自适应深色/浅色模式 */
.submit-card {
  background: var(--md-code-bg-color, rgba(0, 0, 0, 0.05));
  border: 1px solid var(--md-default-fg-color--lightest, rgba(255, 255, 255, 0.1));
  border-radius: var(--base-border-radius, 8px);
  padding: 1.5rem;
  margin: 1.2rem 0;
}
.form-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-bottom: 1rem;
}
.form-group {
  margin-bottom: 1.2rem;
}
.form-group label {
  display: block;
  font-weight: 600;
  font-size: 0.85rem;
  margin-bottom: 0.4rem;
  color: var(--md-default-fg-color);
}
.required {
  color: var(--md-typeset-a-color, #e11d48);
}
.field-hint {
  display: block;
  font-size: 0.75rem;
  color: var(--md-default-fg-color--lighter);
  margin-top: 0.3rem;
}
.md-input {
  width: 100%;
  padding: 0.5rem 0.75rem;
  font-size: 0.85rem;
  font-family: inherit;
  color: var(--md-default-fg-color);
  background: var(--md-default-bg-color);
  border: 1px solid var(--md-default-fg-color--lightest);
  border-radius: 4px;
  box-sizing: border-box;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.md-input:focus {
  outline: none;
  border-color: var(--md-primary-fg-color);
  box-shadow: 0 0 0 2px var(--md-primary-fg-color--transparent, rgba(63, 81, 181, 0.2));
}
.file-input {
  width: 100%;
  padding: 0.6rem;
  font-size: 0.82rem;
  color: var(--md-default-fg-color);
  background: var(--md-default-bg-color);
  border: 1px dashed var(--md-default-fg-color--lighter);
  border-radius: 4px;
  box-sizing: border-box;
  cursor: pointer;
}
.submit-btn {
  width: 100%;
  padding: 0.6rem 1.2rem;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  border: none;
  margin-top: 0.5rem;
}
.progress-container {
  margin: 1rem 0;
}
.progress-labels {
  display: flex;
  justify-content: space-between;
  font-size: 0.8rem;
  color: var(--md-default-fg-color--light);
  margin-bottom: 0.3rem;
}
.progress-track {
  width: 100%;
  height: 6px;
  background: var(--md-default-fg-color--lightest);
  border-radius: 3px;
  overflow: hidden;
}
.progress-bar {
  width: 0%;
  height: 100%;
  background: var(--md-primary-fg-color);
  transition: width 0.2s ease;
}
.status-alert {
  padding: 0.8rem 1rem;
  border-radius: 4px;
  font-size: 0.85rem;
  margin: 1rem 0;
  line-height: 1.5;
}
.status-success {
  background: rgba(34, 197, 94, 0.15);
  border: 1px solid rgba(34, 197, 94, 0.4);
  color: #22c55e;
}
.status-error {
  background: rgba(239, 68, 68, 0.15);
  border: 1px solid rgba(239, 68, 68, 0.4);
  color: #ef4444;
}
</style>

<script>
  (function initApiUrl() {
    const hostname = window.location.hostname;
    const input = document.getElementById('backendApiUrl');
    if (input && hostname && hostname !== 'localhost' && hostname !== '127.0.0.1' && !hostname.includes('github.io')) {
      input.value = `http://${hostname}:8090/api/upload`;
    }
  })();

  function handleFormSubmit(e) {
    e.preventDefault();

    const studentName = document.getElementById('student_name').value.trim();
    const studentClass = document.getElementById('student_class').value.trim();
    const experimentName = document.getElementById('experiment_name').value.trim();
    const notes = document.getElementById('notes').value.trim();
    const pptFileInput = document.getElementById('ppt_file');
    const photoFilesInput = document.getElementById('photo_files');
    const apiUrl = document.getElementById('backendApiUrl').value.trim();

    if (!pptFileInput.files || pptFileInput.files.length === 0) {
      alert('请上传课件 PPT 或 PDF 文件');
      return;
    }
    if (!photoFilesInput.files || photoFilesInput.files.length === 0) {
      alert('请至少上传一张实验实拍照片');
      return;
    }

    const formData = new FormData();
    formData.append('student_name', studentName);
    formData.append('student_class', studentClass);
    formData.append('experiment_name', experimentName);
    formData.append('notes', notes);
    formData.append('ppt_file', pptFileInput.files[0]);

    for (let i = 0; i < photoFilesInput.files.length; i++) {
      formData.append('photo_files', photoFilesInput.files[i]);
    }

    const submitBtn = document.getElementById('submitBtn');
    const progressContainer = document.getElementById('progressContainer');
    const progressBar = document.getElementById('progressBar');
    const progressText = document.getElementById('progressText');
    const statusAlert = document.getElementById('statusAlert');

    submitBtn.disabled = true;
    submitBtn.style.opacity = '0.6';
    progressContainer.style.display = 'block';
    progressBar.style.width = '0%';
    progressText.innerText = '0%';
    statusAlert.style.display = 'none';

    const xhr = new XMLHttpRequest();
    xhr.open('POST', apiUrl, true);

    xhr.upload.onprogress = function(evt) {
      if (evt.lengthComputable) {
        const percent = Math.round((evt.loaded / evt.total) * 100);
        progressBar.style.width = percent + '%';
        progressText.innerText = percent + '%';
      }
    };

    xhr.onload = function() {
      submitBtn.disabled = false;
      submitBtn.style.opacity = '1';
      progressContainer.style.display = 'none';

      if (xhr.status >= 200 && xhr.status < 300) {
        try {
          const res = JSON.parse(xhr.responseText);
          statusAlert.className = 'status-alert status-success';
          statusAlert.style.display = 'block';
          statusAlert.innerHTML = `<strong>投递成功</strong><br>${res.message || '素材已传输至本地后台，AI 即将开始处理。'}`;
          document.getElementById('submissionForm').reset();
        } catch(err) {
          showError('响应解析异常：' + xhr.responseText);
        }
      } else {
        showError(`上传受阻 (HTTP ${xhr.status})，请确认后台接收服务正常运行。`);
      }
    };

    xhr.onerror = function() {
      submitBtn.disabled = false;
      submitBtn.style.opacity = '1';
      progressContainer.style.display = 'none';
      showError('网络连接失败，无法连接至本地接收端。请确认接收服务已开启。');
    };

    function showError(msg) {
      statusAlert.className = 'status-alert status-error';
      statusAlert.style.display = 'block';
      statusAlert.innerHTML = `<strong>传输异常</strong><br>${msg}`;
    }

    xhr.send(formData);
  }
</script>
