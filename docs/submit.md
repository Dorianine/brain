# 实验报告素材投递

!!! info "投递须知"
    本投递通道用于接收实验课件（PPT / PDF）及实验实拍图像（如微孔板显色、试纸条拍照等）。上传后素材将直接流式传输至本地后台，由 AI Agent 自动读取素材并完成符合杭师大规范的排版报告。

<div class="submit-card" markdown>

<form id="submissionForm">

<div class="form-grid">
  <div class="form-group">
    <label for="student_name">学生姓名 <span class="required">*</span></label>
    <input type="text" id="student_name" class="md-input" placeholder="如：张三">
  </div>
  <div class="form-group">
    <label for="student_class">班级 / 学号</label>
    <input type="text" id="student_class" class="md-input" placeholder="如：护理25 / 3220xxxx">
  </div>
  <div class="form-group">
    <label for="experiment_name">实验项目 <span class="required">*</span></label>
    <input type="text" id="experiment_name" class="md-input" value="免疫标记技术" placeholder="如：免疫标记技术">
  </div>
</div>

<div class="form-group">
  <label for="ppt_file">实验课件（PPT / PDF） <span class="required">*</span></label>
  <input type="file" id="ppt_file" class="file-input" accept=".pptx,.ppt,.pdf">
  <span class="field-hint">支持 .pptx, .ppt, .pdf 格式文件</span>
</div>

<div class="form-group">
  <label for="photo_files">实验实拍图像（支持多选） <span class="required">*</span></label>
  <input type="file" id="photo_files" class="file-input" accept="image/*" multiple>
  <span class="field-hint">支持上传手机实拍微孔板显色、试纸条条带等照片</span>
</div>

<div class="form-group">
  <label for="notes">特殊要求与现象备注（选填）</label>
  <textarea id="notes" class="md-input" rows="3" placeholder="例如：老师强调讨论部分重点分析洗板误差；或记录特定孔位淡黄深浅等..."></textarea>
</div>

<div id="progressContainer" class="progress-container" style="display:none;">
  <div class="progress-labels">
    <span id="progressPhase">正在传输数据流...</span>
    <span id="progressText">0%</span>
  </div>
  <div class="progress-track">
    <div id="progressBar" class="progress-bar"></div>
  </div>
</div>

<div id="statusAlert" class="status-alert" style="display:none;"></div>
<div id="debugStatus" style="font-size:0.85rem; margin:10px 0; text-align:center; min-height:1.2rem; color:var(--md-default-fg-color--lighter);"></div>

<button type="button" id="submitBtn" onclick="handleFormSubmit(event)" class="md-button md-button--primary submit-btn">
  提交素材数据流
</button>

</form>

</div>

---

## 已生成的报告

<div id="reportsContainer" class="reports-container">
  <div style="font-size:0.85rem; color:var(--md-default-fg-color--lighter);">正在加载已生成的报告...</div>
</div>

---

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
.reports-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin: 1.2rem 0;
}
.report-card-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--md-code-bg-color, rgba(0, 0, 0, 0.05));
  border: 1px solid var(--md-default-fg-color--lightest, rgba(255, 255, 255, 0.1));
  border-radius: var(--base-border-radius, 8px);
  padding: 12px 16px;
  gap: 12px;
}
.report-card-item:hover {
  border-color: var(--md-primary-fg-color);
}
.report-info-title {
  font-weight: 600;
  font-size: 0.92rem;
  color: var(--md-default-fg-color);
  margin-bottom: 3px;
}
.report-info-meta {
  font-size: 0.78rem;
  color: var(--md-default-fg-color--lighter);
}
.report-dl-btn {
  font-size: 0.82rem;
  padding: 4px 14px;
  text-decoration: none;
  font-weight: 600;
  white-space: nowrap;
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

  window.handleFormSubmit = function(e) {
    try {
      if (e && e.preventDefault) e.preventDefault();

      const submitBtn = document.getElementById('submitBtn');
      if (submitBtn) {
        submitBtn.innerText = '正在准备打包文件...';
      }

      const studentName = (document.getElementById('student_name').value || '').trim();
      const studentClass = (document.getElementById('student_class').value || '').trim();
      const experimentName = (document.getElementById('experiment_name').value || '').trim();
      const notes = (document.getElementById('notes').value || '').trim();
      const pptFileInput = document.getElementById('ppt_file');
      const photoFilesInput = document.getElementById('photo_files');
      const apiUrl = (document.getElementById('backendApiUrl').value || '').trim();

      const progressContainer = document.getElementById('progressContainer');
      const progressBar = document.getElementById('progressBar');
      const progressText = document.getElementById('progressText');
      const statusAlert = document.getElementById('statusAlert');

      function showInlineError(msg, focusId) {
        const debugStatus = document.getElementById('debugStatus');
        if (debugStatus) {
          debugStatus.innerText = msg;
          debugStatus.style.color = '#ef4444';
        }
        if (statusAlert) {
          statusAlert.className = 'status-alert status-error';
          statusAlert.style.display = 'block';
          statusAlert.innerHTML = `<strong>提示：</strong>${msg}`;
          statusAlert.scrollIntoView({ behavior: 'smooth', block: 'center' });
        }
        if (focusId) {
          const el = document.getElementById(focusId);
          if (el) el.focus();
        }
        if (submitBtn) {
          submitBtn.disabled = false;
          submitBtn.innerText = '提交素材数据流';
          submitBtn.style.opacity = '1';
        }
      }

      if (!studentName) {
        showInlineError('请填写【学生姓名】', 'student_name');
        return;
      }

      if (!experimentName) {
        showInlineError('请填写【实验项目名称】', 'experiment_name');
        return;
      }

      if (!pptFileInput.files || pptFileInput.files.length === 0) {
        showInlineError('请选择【实验课件（PPT / PDF）】文件', 'ppt_file');
        return;
      }
      if (!photoFilesInput.files || photoFilesInput.files.length === 0) {
        showInlineError('请选择【实验实拍图像】照片', 'photo_files');
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

      if (submitBtn) {
        submitBtn.disabled = true;
        submitBtn.style.opacity = '0.6';
        submitBtn.innerText = '正在流式传输中...';
      }
      if (progressContainer) progressContainer.style.display = 'block';
      if (progressBar) progressBar.style.width = '0%';
      if (progressText) progressText.innerText = '0%';
      if (statusAlert) statusAlert.style.display = 'none';

      const xhr = new XMLHttpRequest();
      xhr.open('POST', apiUrl, true);

      xhr.upload.onprogress = function(evt) {
        if (evt.lengthComputable && progressBar && progressText) {
          const percent = Math.round((evt.loaded / evt.total) * 100);
          progressBar.style.width = percent + '%';
          progressText.innerText = percent + '%';
          const debugStatus = document.getElementById('debugStatus');
          if (debugStatus) {
            if (percent >= 100) {
              debugStatus.innerText = '数据已推送完毕 (100%)，正在后台排版生成 Word 报告，请稍候约 3 秒...';
            } else {
              debugStatus.innerText = '正在传输数据流 (' + percent + '%)...';
            }
          }
        }
      };

      xhr.onload = function() {
        if (submitBtn) {
          submitBtn.disabled = false;
          submitBtn.style.opacity = '1';
          submitBtn.innerText = '提交素材数据流';
        }
        if (progressContainer) progressContainer.style.display = 'none';

        if (xhr.status >= 200 && xhr.status < 300) {
          try {
            const res = JSON.parse(xhr.responseText);
            const folderName = res.folder;
            const baseDomain = apiUrl.replace('/api/upload', '');

            if (statusAlert) {
              statusAlert.className = 'status-alert status-success';
              statusAlert.style.display = 'block';
              statusAlert.innerHTML = '<strong>素材已送达</strong><br>Gemini 3.8 Flash High 正在深度审阅课件与实拍图，正在为您定制起草实验报告...';
              statusAlert.scrollIntoView({ behavior: 'smooth', block: 'center' });
            }

            let pollCount = 0;
            const pollTimer = setInterval(() => {
              pollCount++;
              fetch(`${baseDomain}/api/check_status/${folderName}`)
                .then(r => r.json())
                .then(st => {
                  if (st.status === 'completed') {
                    clearInterval(pollTimer);
                    const dlUrl = baseDomain + (st.docx_url || `/download/${folderName}/${encodeURIComponent(st.docx_filename)}`);
                    statusAlert.className = 'status-alert status-success';
                    statusAlert.innerHTML = `<strong>投递成功，报告已由 Gemini 3.8 Flash High 撰写完毕</strong><br>已按杭师大规范与《写作风格》排版完成。<div style="margin-top:14px;"><a href="${dlUrl}" target="_blank" class="md-button md-button--primary" style="display:inline-block; text-decoration:none; font-weight:bold; padding:8px 16px;">下载已生成的实验报告 (.docx)</a></div>`;
                    const debugStatus = document.getElementById('debugStatus');
                    if (debugStatus) debugStatus.innerText = 'Gemini 3.8 Flash High 写作排版完成！请点击上方按钮下载报告。';
                    loadGeneratedReports();
                  } else if (pollCount > 100) {
                    clearInterval(pollTimer);
                  }
                })
                .catch(() => {});
            }, 3000);
          } catch(e) {
            if (statusAlert) {
              statusAlert.className = 'status-alert status-success';
              statusAlert.style.display = 'block';
              statusAlert.innerHTML = '<strong>投递成功</strong><br>素材已传输至本地后台。';
            }
          }
          const form = document.getElementById('submissionForm');
          if (form) form.reset();
        } else {
          showError(`上传受阻 (HTTP ${xhr.status})，请确认后台接收服务正常运行。`);
        }
      };

      xhr.onerror = function() {
        if (submitBtn) {
          submitBtn.disabled = false;
          submitBtn.style.opacity = '1';
          submitBtn.innerText = '提交素材数据流';
        }
        if (progressContainer) progressContainer.style.display = 'none';
        showError('网络连接失败，无法连接至本地接收端。请确认接收服务已开启。');
      };

      function showError(msg) {
        if (statusAlert) {
          statusAlert.className = 'status-alert status-error';
          statusAlert.style.display = 'block';
          statusAlert.innerHTML = `<strong>传输异常：</strong>${msg}`;
        }
      }

      xhr.send(formData);
    } catch (err) {
      console.error(err);
    }
  };

  function loadGeneratedReports() {
    const input = document.getElementById('backendApiUrl');
    const apiUrl = (input ? input.value : '').trim();
    const baseDomain = apiUrl.replace('/api/upload', '');
    const container = document.getElementById('reportsContainer');
    if (!container || !baseDomain) return;

    fetch(`${baseDomain}/api/reports`)
      .then(r => r.json())
      .then(data => {
        if (!data.reports || data.reports.length === 0) {
          container.innerHTML = '<div style="font-size:0.85rem; color:var(--md-default-fg-color--lighter);">暂无已生成的报告记录。</div>';
          return;
        }
        container.innerHTML = data.reports.map(rpt => `
          <div class="report-card-item">
            <div>
              <div class="report-info-title">${escapeHtml(rpt.experiment_name || '实验报告')} · ${escapeHtml(rpt.student_name || '未知同学')}</div>
              <div class="report-info-meta">完成时间：${escapeHtml(rpt.completed_at || '-')} &nbsp;|&nbsp; 班级/学号：${escapeHtml(rpt.student_class || '-')}</div>
            </div>
            <a href="${baseDomain + rpt.download_url}" target="_blank" class="md-button md-button--primary report-dl-btn">下载 Word</a>
          </div>
        `).join('');
      })
      .catch(() => {
        container.innerHTML = '<div style="font-size:0.85rem; color:var(--md-default-fg-color--lighter);">暂未连接到本地接收端。</div>';
      });
  }

  function escapeHtml(str) {
    if (!str) return '';
    return String(str).replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;');
  }

  setTimeout(loadGeneratedReports, 500);
</script>
