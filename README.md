---
title: About Aidemofashi
date: 2026-02-06 14:36:41
lazyload: false
---
<div id="profile-header" style="display: flex; align-items: center; gap: 20px; margin-bottom: 10px;">
  <img src="./avatar.jpg" width="75" style="border-radius: 50%; border: 3px solid #66ccff;" onerror="this.src='/images/default-avatar.jpg'"><h2>你好 👋 <sub>Hello!</sub></h2>
</div>

Here is *Aidemofashi*.

📙 Year 2024 student at university
💻 Focusing on cybersecurity & CTF (Web exploitation)
🎭 Member of CTF team [GWWAFZ](https://gwwafz.online/)
✏ Wrote some light novels on <img src="https://www.ciweimao.com/resources/image/icon/CiWeiMao_Icon_32_R.png" width="16" style="vertical-align: middle; margin-right: 4px;">[Ciweimao](https://www.ciweimao.com/book/100460679)

---

🔗 Find me on:

><img src="https://github.com/favicon.ico" width="16" style="vertical-align: middle; margin-right: 4px;"> [GitHub](https://github.com/aidemofashi/) | aidemofashi
> <img src="https://www.bilibili.com/favicon.ico" width="16" style="vertical-align: middle; margin-right: 4px;"> [Bilibili](https://space.bilibili.com/455215669/) | Aidemofashi_

> QQ: 3525417592
> Email: zhonghuaiyu2019@163.com

---

💗 Happy to do:
>Wacth Anime 
>Video Game 
>Reading
>Make Friend

---

## Bangumi 动画记录



#### 📺 在看
<div id="watching-list" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 15px; margin: 15px 0;">
  <p style="grid-column: span 2;">⏳ 正在加载...</p>
</div>

#### ⭐ 想看
<div id="wishlist-list" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 15px; margin: 15px 0;">
  <p style="grid-column: span 2;">⏳ 正在加载...</p>
</div>

#### ✅ 看过
<div id="watched-list" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 15px; margin: 15px 0;">
  <p style="grid-column: span 2;">⏳ 正在加载...</p>
</div>

<style>
.bangumi-card {
  text-align: center;
  padding: 12px;
  background: #f8f9fa;
  border-radius: 8px;
  transition: transform 0.2s;
}
.bangumi-card:hover {
  transform: translateY(-3px);
}
.bangumi-card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 4px;
  margin-bottom: 8px;
}
.bangumi-card-title {
  font-weight: bold;
  font-size: 14px;
  margin-bottom: 4px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.bangumi-card-meta {
  font-size: 12px;
  color: #666;
}
.bangumi-card-score {
  display: flex;
  justify-content: space-between;
  font-size: 12px;
  color: #999;
}
</style>

<script>
const API_BASE = 'https://api.bgm.tv/v0/users/1212399/collections';
const LIMIT = 15; // 每个分类显示15个

function loadBangumi(type, containerId) {
  fetch(`${API_BASE}?subject_type=2&type=${type}&limit=${LIMIT}&offset=0`)
    .then(response => response.json())
    .then(data => {
      const container = document.getElementById(containerId);
      container.innerHTML = '';
      
      if (!data.data || data.data.length === 0) {
        container.innerHTML = '<p style="grid-column: span 2;">📭 暂无数据</p>';
        return;
      }
      
      data.data.forEach(item => {
        const subject = item.subject;
        const img = subject.images?.medium || subject.images?.grid || subject.images?.small;
        const name = subject.name_cn || subject.name;
        const score = subject.score || 'N/A';
        const rank = subject.rank ? `#${subject.rank}` : '';
        const date = subject.date || '';
        const rate = item.rate || '';
        
        const card = document.createElement('div');
        card.className = 'bangumi-card';
        card.innerHTML = `
          <a href="https://bgm.tv/subject/${subject.id}" target="_blank" style="text-decoration: none; color: inherit;">
            <img src="${img}" alt="${name}" loading="lazy">
            <div class="bangumi-card-title">${name}</div>
            <div class="bangumi-card-meta">${date}</div>
            <div class="bangumi-card-score">
              <span>⭐ ${score}</span>
              ${rank ? `<span>${rank}</span>` : ''}
            </div>
            ${rate ? `<div style="font-size: 11px; color: #ff6600; margin-top: 4px;">我的评分: ${rate}</div>` : ''}
          </a>
        `;
        container.appendChild(card);
      });
    })
    .catch(error => {
      document.getElementById(containerId).innerHTML = '<p style="grid-column: span 2;">❌ 加载失败</p>';
      console.error('Bangumi API error:', error);
    });
}

// 加载三个列表
loadBangumi(3, 'watching-list');   // 在看
loadBangumi(1, 'wishlist-list');   // 想看
loadBangumi(2, 'watched-list');    // 看过
</script>
