    </div>
    
    <div class="admin-grid" style="margin-top:12px">
      <div class="card">
        <h3>🖼️ Leadership Customization</h3>
        <p class="muted small">আগে থেকে থাকা leadership-গুলোর নাম/পদ আবার লিখতে হবে না। প্রতিটি ব্যক্তির <b>Change Photo</b> দিয়ে শুধু ছবি বদলাতে পারবেন। চাইলে নাম, পদ ও এলাকা-ও Edit করে Save করতে পারবেন।</p>
        <div id="leadershipAdminList" class="release-list">
          <div class="empty">Leadership লোড হচ্ছে…</div>
        </div>
        <div id="leadStatus" class="status"></div>
      </div>

      <div class="card">
        <h3>Social Worker</h3>
        <form id="workerForm">
          <input id="workerName" placeholder="কর্মীর নাম" required>
          <input id="workerArea" placeholder="এলাকা">
          <input id="workerWard" placeholder="ওয়ার্ড">
          <input id="workerPhoto" type="file" accept="image/*">
          <button class="btn primary">Save Worker</button>
          <div id="workerStatus" class="status"></div>
        </form>
      </div>

      <div class="card">
        <h3>Activity Verification</h3>
        <form id="activityAdminForm">
          <input id="activityId" placeholder="Activity UUID" required>
          <input id="activityPoints" type="number" min="0" placeholder="Points" required>
          <button class="btn primary">Approve + Points</button>
          <div id="activityAdminStatus" class="status"></div>
        </form>
      </div>

      <div class="card">
        <h3>Breaking Ticker</h3>
        <form id="tickerForm">
          <input id="tickerInput" placeholder="Ticker message" required>
          <button class="btn primary">Publish Ticker</button>
          <div id="tickerAdminStatus" class="status"></div>
        </form>
      </div>

      <div class="card">
        <h3>🗳️ Poll Management</h3>
        <form id="pollAdminForm">
          <input id="pollQuestion" maxlength="300" placeholder="Poll question" required>
          <input id="pollA" maxlength="120" placeholder="Option A" required>
          <input id="pollB" maxlength="120" placeholder="Option B" required>
          <button class="btn primary">Publish Poll</button>
          <div id="pollAdminStatus" class="status"></div>
        </form>
      </div>

      <div class="card">
        <h3>🤝 Volunteer Opportunity</h3>
        <form id="volAdminForm">
          <input id="volTitle" maxlength="160" placeholder="কাজের নাম" required>
          <textarea id="volDescription" maxlength="2000" placeholder="কাজের বিবরণ"></textarea>
          <input id="volCategory" maxlength="80" placeholder="Category">
          <input id="volDate" type="datetime-local">
          <input id="volLocation" maxlength="160" placeholder="Location">
          <button class="btn primary">Publish Volunteer Work</button>
          <div id="volAdminStatus" class="status"></div>
        </form>
      </div>

      <div class="card">
        <h3>💡 Feedback Inbox</h3>
        <button class="btn" id="loadIdeasBtn" type="button">Load Latest Ideas</button>
        <div id="ideasAdminList" class="mini" style="margin-top:10px"></div>
      </div>

      <div class="card">
        <h3>📢 Release Publish</h3>
        <form id="releaseForm">
          <input id="releaseTitle" placeholder="Release / Notice title" required>
          <textarea id="releaseBody" placeholder="বিস্তারিত লিখুন"></textarea>
          <input id="releaseFile" type="file" accept="image/*,.pdf,.doc,.docx">
          <button class="btn primary">Publish Release</button>
          <div id="releaseStatus" class="status"></div>
        </form>
      </div>

      <div class="card">
        <h3>📱 Facebook Live / Social Video</h3>
        <form id="socialForm">
          <input id="socialTitle" placeholder="ভিডিওর শিরোনাম" required>
          <input id="socialUrl" type="url" placeholder="Facebook Live video URL" required>
          <textarea id="socialDescription" placeholder="সংক্ষিপ্ত বিবরণ"></textarea>
          <input id="socialThumb" type="file" accept="image/*">
          <button class="btn primary">Publish Video</button>
          <div id="socialStatus" class="status"></div>
        </form>
      </div>
    </div>
  </section>
</main>

<footer>
  <div class="wrap">© BJYM South Howrah 3 No Mondal</div>
</footer>

<dialog id="loginDialog">
  <button class="close" id="closeLogin">×</button>
  <h3>Admin Login</h3>
  <form id="loginForm">
    <label>Login ID</label>
    <input id="email" type="email" autocomplete="username" required>
    <label>Password</label>
    <input id="password" type="password" autocomplete="current-password" required>
    <button class="btn primary" type="submit">Sign in</button>
    <div id="loginStatus" class="status"></div>
  </form>
</dialog>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script>
  const U = "https://udiggdolyxexducoaimz.supabase.co";
  const K = "sb_publishable_Miuh6QQVWjXRlU1-Hu2PaA_urnDXk7q";
  const db = supabase.createClient(U, K, {
    auth: { persistSession: true, autoRefreshToken: true, detectSessionInUrl: true }
  });

  const leaders = [
    ["নরেন্দ্র দামোদরদাস মোদী", "ভারতের প্রধানমন্ত্রী"],
    ["শ্রী শুভেন্দু অধিকারী", "পশ্চিমবঙ্গের মুখ্যমন্ত্রী"],
    ["শ্রী শমিক ভট্টাচার্য", "পশ্চিমবঙ্গ রাজ্য সভাপতি — ভারতীয় জনতা পার্টি"],
    ["শ্রী ইন্দ্রনীল খাঁ", "ভারতীয় জনতা যুব মোর্চার রাজ্য সভাপতি"]
  ];
  const mondal = [
    ["শ্রীযুক্ত রবিন পাল মহোদয়", "ভারতীয় জনতা পার্টির মণ্ডল সভাপতি"],
    ["শ্রী কৃষ্ণেন্দু পোল্ল্যে (সঞ্জু)", "ভারতীয় জনতা যুব মোর্চার সভাপতি"]
  ];

  const $ = x => document.getElementById(x);
  const esc = x => String(x ?? "").replace(/[&<>"']/g, c => ({
    "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;"
  }[c]));
  const ini = x => x.trim().split(/\s+/).slice(0, 2).map(y => y[0]).join("");

  function people(id, a) {
    $(id).innerHTML = a.map(x => `
      <article class="card">
        <div class="avatar">${esc(ini(x[0]))}</div>
        <h3>${esc(x[0])}</h3>
        <div class="role">${esc(x[1])}</div>
      </article>
    `).join("");
  }
  people("leadersGrid", leaders);
  people("mondalGrid", mondal);

  async function loadLeadership() {
    let r = await db.from("leadership_profiles").select("*").eq("active", true).order("sort_order").order("created_at");
    if (r.error) {
      $("leadersGrid").innerHTML = $("mondalGrid").innerHTML = `<div class="card empty">Leadership load error: ${esc(r.error.message)}</div>`;
      return;
    }
    let a = r.data || [];
    let top = a.filter(x => x.level !== "local");
    let local = a.filter(x => x.level === "local");

    function card(x) {
      return `
        <article class="card">
          <div class="avatar">${x.photo_path ? `<img class="leader-photo" src="${esc(publicUrl(x.photo_path))}" alt="">` : esc(ini(x.name || "?"))}</div>
          <h3>${esc(x.name)}</h3>
          <div class="role">${esc(x.title || "")}</div>
          ${x.area ? `<div class="muted small">${esc(x.area)}</div>` : ""}
        </article>
      `;
    }

    $("leadersGrid").innerHTML = top.length ? top.map(card).join("") : `<div class="card empty">Leadership এখনও যোগ করা হয়নি।</div>`;
    $("mondalGrid").innerHTML = local.length ? local.map(card).join("") : `<div class="card empty">মণ্ডল leadership এখনও যোগ করা হয়নি।</div>`;
    if (document.querySelector("#adminPanel.admin.show")) renderLeadershipAdmin(a);
  }

  function renderLeadershipAdmin(a) {
    $("leadershipAdminList").innerHTML = a.length ? a.map(x => `
      <div class="card" style="margin-top:8px">
        <div style="display:flex;gap:12px;align-items:center">
          <div class="avatar" style="margin:0;flex:none">
            ${x.photo_path ? `<img class="leader-photo" src="${esc(publicUrl(x.photo_path))}" alt="">` : esc(ini(x.name || "?"))}
          </div>
          <div style="flex:1">
            <b>${esc(x.name)}</b>
            <div class="mini">${esc(x.title || "")}</div>
          </div>
        </div>
        <form class="lead-edit" data-id="${x.id}" style="margin-top:10px">
          <input name="name" value="${esc(x.name)}" placeholder="নাম" required>
          <input name="title" value="${esc(x.title)}" placeholder="পদ" required>
          <input name="area" value="${esc(x.area || "")}" placeholder="এলাকা (ঐচ্ছিক)">
          <input name="photo" type="file" accept="image/*">
          <div class="actions">
            <button class="btn primary" type="submit">💾 Save Changes</button>
          </div>
          <div class="status"></div>
        </form>
      </div>
    `).join("") : `<div class="empty">Leadership নেই।</div>`;

    document.querySelectorAll(".lead-edit").forEach(f => f.onsubmit = async e => {
      e.preventDefault();
      let st = f.querySelector(".status");
      st.textContent = "Saving…";
      try {
        let d = new FormData(f);
        let patch = {
          name: String(d.get("name") || "").trim(),
          title: String(d.get("title") || "").trim(),
          area: String(d.get("area") || "").trim() || null
        };
        let file = d.get("photo");
        if (file && file.size) patch.photo_path = await uploadImage(file, "leadership");
        let r = await db.from("leadership_profiles").update(patch).eq("id", f.dataset.id);
        st.textContent = r.error ? r.error.message : "Saved successfully.";
        if (!r.error) await loadLeadership();
      } catch (err) {
        st.textContent = err.message;
      }
    });
  }

  function publicUrl(path) {
    if (!path) return "";
    return db.storage.from("social-impact-media").getPublicUrl(path).data.publicUrl;
  }

  async function loadAll() {
    await loadLeadership();

    let m = await db.from("impact_metrics").select("*").eq("active", true).order("sort_order");
    $("impactGrid").innerHTML = (m.data || []).map(x => `
      <div class="card impact-card">
        <div class="impact-number" data-target="${x.value}">0${esc(x.suffix)}</div>
        <div>${esc(x.label)}</div>
      </div>
    `).join("");

    document.querySelectorAll(".impact-number").forEach(el => {
      let n = +el.dataset.target, i = 0, step = Math.max(1, Math.ceil(n / 35));
      let t = setInterval(() => {
        i = Math.min(n, i + step);
        el.textContent = i.toLocaleString("en-IN") + (el.textContent.includes("+") ? "+" : "");
        if (i >= n) clearInterval(t);
      }, 22);
    });

    let l = await db.from("social_leaderboard").select("*").order("karma_points", { ascending: false }).limit(20);
    let rows = l.data || [];
    $("leaderboardList").innerHTML = rows.length ? rows.map((x, i) => `
      <div class="rank">
        <div class="badge">${i < 3 ? ["🥇", "🥈", "🥉"][i] : "#" + (i + 1)}</div>
        ${x.photo_path ? `<img src="${esc(publicUrl(x.photo_path))}">` : `<div class="avatar" style="margin:0;width:58px;height:58px">${esc(ini(x.name || "?"))}</div>`}
        <div>
          <b>${esc(x.name)}</b>
          <div class="muted small">${esc(x.area || "")} ${x.ward_no ? "• Ward " + esc(x.ward_no) : ""}</div>
        </div>
        <div class="points">${Number(x.karma_points || 0)} pts</div>
      </div>
    `).join("") : '<div class="card empty">এখনও কোনও verified service activity নেই।</div>';

    let top = rows[0];
    $("monthlyWinner").innerHTML = top ? `
      <div style="text-align:center">
        <div class="role">WARRIOR OF THE MONTH</div>
        ${top.photo_path ? `<img class="leader-photo" src="${esc(publicUrl(top.photo_path))}">` : ''}
        <h3>${esc(top.name)}</h3>
        <div class="points">${Number(top.karma_points || 0)} Karma Points</div>
      </div>
    ` : '<div class="empty">এই মাসের verified activity এখনও নেই।</div>';

    let a = await db.from("service_activities").select("*").eq("status", "approved").order("created_at", { ascending: false }).limit(12);
    $("activityList").innerHTML = (a.data || []).length ? (a.data || []).map(x => `
      <article class="card">
        <h3>${esc(x.title || x.activity_type || "সমাজসেবা কার্যক্রম")}</h3>
        <p>${esc(x.description || "")}</p>
        ${x.photo_path ? `<img src="${esc(publicUrl(x.photo_path))}">` : ""}
        <div class="muted">${esc(x.area || "")} ${x.ward_no ? "• Ward " + esc(x.ward_no) : ""} • <b>${Number(x.points || 0)} points</b></div>
      </article>
    `).join("") : '<div class="card empty">এখনও কোনও approved activity নেই।</div>';

    let e = await db.from("events").select("*").order("event_date", { ascending: true });
    $("eventsList").innerHTML = e.error || !e.data?.length ? '<div class="card empty">কোনও কর্মসূচি এখনও প্রকাশিত হয়নি।</div>' : e.data.map(x => `
      <article class="card">
        <h3>${esc(x.title)}</h3>
        <p>${esc(x.description || "")}</p>
        <p class="muted">${esc(x.event_date || "")} ${esc(x.location || "")}</p>
      </article>
    `).join("");

    let c = await db.from("emergency_contacts").select("*").eq("active", true).order("sort_order");
    $("contactsGrid").innerHTML = (c.data || []).length ? (c.data || []).map(x => `
      <article class="card">
        <h3>${esc(x.service_name)}</h3>
        <a class="btn primary" href="tel:${esc(x.phone)}">📞 ${esc(x.phone)}</a>
        <p class="muted">${esc(x.area || "")} ${esc(x.note || "")}</p>
      </article>
    `).join("") : '<div class="card empty">Admin এখনও emergency contacts যোগ করেননি।</div>';

    let s = await db.from("government_schemes").select("*").eq("active", true);
    $("schemesGrid").innerHTML = (s.data || []).length ? (s.data || []).map(x => `
      <article class="card">
        <h3>${esc(x.title || x.name || "")}</h3>
        <p>${esc(x.description || x.details || "")}</p>
      </article>
    `).join("") : '<div class="card empty">সরকারি প্রকল্পের তথ্য শীঘ্রই যোগ করা হবে।</div>';

    let q = await db.from("inspiration_quotes").select("*").eq("active", true).order("sort_order");
    $("quotesGrid").innerHTML = (q.data || []).length ? (q.data || []).map(x => `
      <article class="card">
        <p>“${esc(x.quote_text)}”</p>
        <b>${esc(x.person_name)}</b>
      </article>
    `).join("") : '<div class="card empty">অনুপ্রেরণামূলক উক্তি শীঘ্রই যোগ করা হবে।</div>';

    let rel = await db.from("releases").select("*").eq("published", true).order("created_at", { ascending: false }).limit(30);
    $("releaseList").innerHTML = rel.error || !rel.data?.length ? '<div class="card empty">এখনও কোনও প্রকাশনা প্রকাশিত হয়নি।</div>' : rel.data.map(x => `
      <article class="card release-card">
        <h3>📢 ${esc(x.title)}</h3>
        <p>${esc(x.body || "")}</p>
        ${x.file_path ? `<a class="btn primary" target="_blank" rel="noopener" href="${esc(publicUrl(x.file_path))}">📎 ${esc(x.file_name || "ডকুমেন্ট দেখুন")}</a>` : ""}
        <div class="muted small">${new Date(x.created_at).toLocaleString("bn-IN")}</div>
      </article>
    `).join("");

    let sm = await db.from("social_media_posts").select("*").eq("active", true).order("created_at", { ascending: false }).limit(30);
    $("socialMediaList").innerHTML = sm.error || !sm.data?.length ? '<div class="card empty">এখনও কোনও social media video প্রকাশিত হয়নি।</div>' : sm.data.map(x => {
      let u = String(x.video_url || "");
      let embed = u.includes("facebook.com")
        ? `<a class="btn primary social-link" target="_blank" rel="noopener" href="${esc(u)}">▶️ Facebook Live ভিডিও দেখুন</a>`
        : `<a class="btn primary social-link" target="_blank" rel="noopener" href="${esc(u)}">▶️ ভিডিও দেখুন</a>`;
      return `
        <article class="card social-card">
          ${x.thumbnail_path ? `<img class="feed img" src="${esc(publicUrl(x.thumbnail_path))}" alt="">` : ""}
          <h3>📺 ${esc(x.title)}</h3>
          <p>${esc(x.description || "")}</p>
          ${embed}
          <div class="muted small">${esc(x.platform || "social media")} • ${new Date(x.created_at).toLocaleString("bn-IN")}</div>
        </article>
      `;
    }).join("");

    let t = await db.from("breaking_tickers").select("message").eq("active", true).order("sort_order").limit(5);
    $("tickerText").textContent = (t.data || []).map(x => x.message).join(" • ") || "সমাজসেবামূলক কার্যক্রমের আপডেট এখানে প্রদর্শিত হবে।";

    let p = await db.from("public_posts").select("display_name,message,created_at").eq("status", "approved").order("created_at", { ascending: false });
    $("postsList").innerHTML = p.error || !p.data?.length ? '<div class="card empty">এখনও কোনও approved post নেই।</div>' : p.data.map(x => `
      <article class="card">
        <b>${esc(x.display_name)}</b>
        <p>${esc(x.message)}</p>
      </article>
    `).join("");
  }

  $("postForm").onsubmit = async e => {
    e.preventDefault();
    $("postStatus").textContent = "জমা হচ্ছে…";
    let r = await db.from("public_posts").insert({
      display_name: $("displayName").value.trim(),
      message: $("message").value.trim(),
      status: "pending"
    });
    $("postStatus").textContent = r.error ? "জমা দেওয়া যায়নি।" : "বার্তা জমা হয়েছে। Admin approval-এর পর প্রকাশিত হবে।";
    if (!r.error) e.target.reset();
  };

  $("adminBtn").onclick = () => $("loginDialog").showModal();
  $("closeLogin").onclick = () => $("loginDialog").close();

  async function openAdminSession() {
    let q = await db.auth.getSession();
    let u = q.data.session?.user;
    if (!u) return false;
    let a = await db.from("admin_profiles").select("display_name,role").eq("user_id", u.id).maybeSingle();
    if (a.error || !a.data) return false;
    $("loginDialog").close();
    $("adminPanel").classList.add("show");
    $("adminStatus").textContent = "Logged in as " + (a.data.display_name || "Admin");
    let l = await db.from("leadership_profiles").select("*").eq("active", true).order("sort_order").order("created_at");
    if (!l.error) renderLeadershipAdmin(l.data || []);
    return true;
  }

  $("loginForm").onsubmit = async e => {
    e.preventDefault();
    $("loginStatus").textContent = "Signing in…";
    let email = $("email").value.trim().toLowerCase();
    let password = $("password").value;
    let r = await db.auth.signInWithPassword({ email, password });
    if (r.error) {
      $("loginStatus").textContent = "Login failed: " + (r.error.message || "Invalid login details");
      return;
    }
    let ok = await openAdminSession();
    if (!ok) {
      await db.auth.signOut();
      $("loginStatus").textContent = "Login successful, but this account is not registered as an Admin.";
      return;
    }
  };

  db.auth.onAuthStateChange((event, session) => {
    if (session) setTimeout(() => openAdminSession(), 0);
  });

  async function uploadImage(file, path) {
    if (!file) return null;
    let ext = (file.name.split(".").pop() || "jpg").toLowerCase();
    let full = path + "/" + crypto.randomUUID() + "." + ext;
    let r = await db.storage.from("social-impact-media").upload(full, file, { upsert: false });
    if (r.error) throw r.error;
    return full;
  }

  $("workerForm").onsubmit = async e => {
    e.preventDefault();
    $("workerStatus").textContent = "Saving…";
    try {
      let path = await uploadImage($("workerPhoto").files[0], "workers");
      let r = await db.from("social_workers").insert({
        name: $("workerName").value.trim(),
        area: $("workerArea").value.trim(),
        ward_no: $("workerWard").value.trim(),
        photo_path: path
      });
      $("workerStatus").textContent = r.error ? r.error.message : "Worker saved.";
      if (!r.error) e.target.reset();
    } catch (err) {
      $("workerStatus").textContent = err.message;
    }
  };

  $("activityAdminForm").onsubmit = async e => {
    e.preventDefault();
    let r = await db.from("service_activities").update({
      status: "approved",
      points: Number($("activityPoints").value),
      verified_at: new Date().toISOString()
    }).eq("id", $("activityId").value.trim());
    $("activityAdminStatus").textContent = r.error ? r.error.message : "Approved and points saved.";
    if (!r.error) loadAll();
  };

  $("tickerForm").onsubmit = async e => {
    e.preventDefault();
    let r = await db.from("breaking_tickers").insert({
      message: $("tickerInput").value.trim(),
      active: true
    });
    $("tickerAdminStatus").textContent = r.error ? r.error.message : "Ticker published.";
    if (!r.error) {
      e.target.reset();
      loadAll();
    }
  };

  $("releaseForm").onsubmit = async e => {
    e.preventDefault();
    $("releaseStatus").textContent = "Publishing…";
    try {
      let f = $("releaseFile").files[0], path = null;
      if (f) path = await uploadImage(f, "releases");
      let r = await db.from("releases").insert({
        title: $("releaseTitle").value.trim(),
        body: $("releaseBody").value.trim(),
        file_path: path,
        file_name: f?.name || null,
        published: true
      });
      $("releaseStatus").textContent = r.error ? r.error.message : "Release published.";
      if (!r.error) {
        e.target.reset();
        loadAll();
      }
    } catch (err) {
      $("releaseStatus").textContent = err.message;
    }
  };

  $("socialForm").onsubmit = async e => {
    e.preventDefault();
    $("socialStatus").textContent = "Publishing…";
    try {
      let f = $("socialThumb").files[0], path = null;
      if (f) path = await uploadImage(f, "social-thumbnails");
      let r = await db.from("social_media_posts").insert({
        platform: "facebook",
        title: $("socialTitle").value.trim(),
        description: $("socialDescription").value.trim(),
        video_url: $("socialUrl").value.trim(),
        thumbnail_path: path,
        active: true
      });
      $("socialStatus").textContent = r.error ? r.error.message : "Video published.";
      if (!r.error) {
        e.target.reset();
        loadAll();
      }
    } catch (err) {
      $("socialStatus").textContent = err.message;
    }
  };

  async function loadPolls() {
    let r = await db.from("polls").select("*").eq("active", true).order("created_at", { ascending: false });
    let a = r.data || [];
    $("pollList").innerHTML = r.error || !a.length ? '<div class="card empty">এখনও কোনও active poll নেই।</div>' : a.map(p => {
      let voted = localStorage.getItem("poll-voted-" + p.id) === "1";
      return `
        <article class="card poll-box">
          <h3>🗳️ ${esc(p.question)}</h3>
          <div class="actions">
            <button class="btn poll-option" ${voted ? 'disabled' : ''} data-poll="${p.id}" data-opt="a">A. ${esc(p.option_a)}</button>
            <button class="btn poll-option" ${voted ? 'disabled' : ''} data-poll="${p.id}" data-opt="b">B. ${esc(p.option_b)}</button>
          </div>
          <div class="mini">${voted ? 'এই ডিভাইস থেকে আপনার ভোট নেওয়া হয়েছে।' : 'এক ক্লিকে একটি অপশন নির্বাচন করুন।'}</div>
        </article>
      `;
    }).join("");

    document.querySelectorAll(".poll-option").forEach(b => b.onclick = async () => {
      let id = b.dataset.poll, opt = b.dataset.opt;
      if (localStorage.getItem("poll-voted-" + id)) return;
      let x = await db.from("poll_votes").insert({ poll_id: id, option_key: opt });
      if (!x.error) {
        localStorage.setItem("poll-voted-" + id, "1");
        loadPolls();
      } else {
        alert("ভোট দেওয়া যায়নি: " + x.error.message);
      }
    });
  }

  async function loadVolunteers() {
    let r = await db.from("volunteer_opportunities").select("*").eq("active", true).order("event_date", { ascending: true });
    let a = r.data || [];
    $("volunteerList").innerHTML = r.error || !a.length ? '<div class="card empty">এখনও কোনও volunteer opportunity প্রকাশিত হয়নি।</div>' : a.map(v => `
      <article class="card vol-box">
        <h3>🤝 ${esc(v.title)}</h3>
        <p>${esc(v.description || "")}</p>
        <div class="muted small">${esc(v.category || "")} ${v.event_date ? '• ' + new Date(v.event_date).toLocaleString("bn-IN") : ''} ${v.location ? '• ' + esc(v.location) : ''}</div>
        <form class="vol-signup" data-id="${v.id}" style="margin-top:10px">
          <input name="name" maxlength="80" placeholder="আপনার নাম" required>
          <input name="phone" maxlength="30" placeholder="Phone">
          <input name="area" maxlength="100" placeholder="এলাকা">
          <input name="group_name" maxlength="100" placeholder="ছোট গ্রুপের নাম (ঐচ্ছিক)">
          <button class="btn primary">🙋 Volunteer হিসেবে যুক্ত হোন</button>
          <div class="status"></div>
        </form>
      </article>
    `).join("");

    document.querySelectorAll(".vol-signup").forEach(f => f.onsubmit = async e => {
      e.preventDefault();
      let d = new FormData(f);
      let r = await db.from("volunteer_signups").insert({
        opportunity_id: f.dataset.id,
        name: d.get("name"),
        phone: d.get("phone"),
        area: d.get("area"),
        group_name: d.get("group_name")
      });
      f.querySelector(".status").textContent = r.error ? r.error.message : "আপনার volunteer request জমা হয়েছে। Admin confirmation-এর পর status update হবে।";
      if (!r.error) f.reset();
    });
  }

  $("ideaForm").onsubmit = async e => {
    e.preventDefault();
    $("ideaStatus").textContent = "পাঠানো হচ্ছে…";
    let r = await db.from("idea_suggestions").insert({
      name: $("ideaName").value.trim() || null,
      contact: $("ideaContact").value.trim() || null,
      subject: $("ideaSubject").value.trim(),
      message: $("ideaMessage").value.trim()
    });
    $("ideaStatus").textContent = r.error ? r.error.message : "আপনার idea/feedback সরাসরি Admin inbox-এ পাঠানো হয়েছে।";
    if (!r.error) e.target.reset();
  };

  $("pollAdminForm").onsubmit = async e => {
    e.preventDefault();
    let r = await db.from("polls").insert({
      question: $("pollQuestion").value.trim(),
      option_a: $("pollA").value.trim(),
      option_b: $("pollB").value.trim(),
      active: true
    });
    $("pollAdminStatus").textContent = r.error ? r.error.message : "Poll published.";
    if (!r.error) {
      e.target.reset();
      loadPolls();
    }
  };

  $("volAdminForm").onsubmit = async e => {
    e.preventDefault();
    let r = await db.from("volunteer_opportunities").insert({
      title: $("volTitle").value.trim(),
      description: $("volDescription").value.trim(),
      category: $("volCategory").value.trim(),
      event_date: $("volDate").value ? new Date($("volDate").value).toISOString() : null,
      location: $("volLocation").value.trim(),
      active: true
    });
    $("volAdminStatus").textContent = r.error ? r.error.message : "Volunteer opportunity published.";
    if (!r.error) {
      e.target.reset();
      loadVolunteers();
    }
  };

  $("loadIdeasBtn").onclick = async () => {
    let r = await db.from("idea_suggestions").select("*").order("created_at", { ascending: false }).limit(30);
    $("ideasAdminList").innerHTML = r.error ? esc(r.error.message) : r.data.length ? r.data.map(x => `
      <div class="card" style="margin-top:8px">
        <b>${esc(x.subject)}</b>
        <div>${esc(x.message)}</div>
        <div class="mini">${esc(x.name || "Anonymous")} • ${esc(x.contact || "")} • ${esc(x.status)}</div>
      </div>
    `).join("") : "No ideas yet.";
  };

  $("logoutBtn").onclick = async () => {
    await db.auth.signOut();
    $("adminPanel").classList.remove("show");
  };

  $("refreshBtn").onclick = loadAll;

  loadAll();
  loadPolls();
  loadVolunteers();
</script>

<section class="card" id="president-contact" style="margin:24px 0;padding:24px;border-radius:22px;background:linear-gradient(135deg,rgba(255,153,0,.14),rgba(19,136,8,.12));border:1px solid rgba(255,153,0,.35);box-shadow:0 12px 35px rgba(0,0,0,.18);text-align:center">
  <h2 style="margin:0 0 8px">📞 সরাসরি সভাপতির সঙ্গে যোগাযোগ</h2>
  <div style="font-size:1.15rem;font-weight:800">শ্রী কৃষ্ণেন্দু পোল্ল্যে (সঞ্জু)</div>
  <div style="font-size:.88rem;opacity:.78;margin:4px 0 16px">ভারতীয় জনতা যুব মোর্চার সভাপতি — সরাসরি যোগাযোগের মাধ্যম</div>
  <div style="display:flex;gap:12px;justify-content:center;flex-wrap:wrap">
    <a href="tel:+917003935754" style="padding:11px 18px;border-radius:12px;text-decoration:none;font-weight:800;background:rgba(2,132,199,.18);color:inherit">📱 +91 7003935754</a>
    <a href="mailto:poileysanju@gmail.com" style="padding:11px 18px;border-radius:12px;text-decoration:none;font-weight:800;background:rgba(236,72,153,.14);color:inherit">✉️ poileysanju@gmail.com</a>
  </div>
  <div style="margin-top:18px;font-size:.9rem;line-height:1.7">
    <b>অঞ্চল:</b> Duiliya, Jhorehat, Panchpara, Thanamakua<br>
    <b>অফিস:</b> Basudevpur, Jhorehat, Howrah-711304
  </div>
</section>

<footer style="text-align:center;padding:24px 16px;margin-top:30px;border-top:1px solid rgba(255,255,255,.12);color:#94a3b8;font-size:14px;">
  প্রীতম দাস কর্তৃক পরিচালিত
</footer>

</body>
</html>
