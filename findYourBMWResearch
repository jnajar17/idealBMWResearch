document.addEventListener("DOMContentLoaded", () => {

const modelSlugs = {
        "BMW 3 Series": "/searchnew.aspx?ModelAndTrim=330i!340i",
        "BMW 5 Series": "/searchnew.aspx?ModelAndTrim=530i!540i",
        "BMW X1": "/searchnew.aspx?ModelAndTrim=X1",
        "BMW X3": "/searchnew.aspx?ModelAndTrim=X3",
        "BMW X5": "/searchnew.aspx?ModelAndTrim=X5",
        "BMW X7": "/searchnew.aspx?ModelAndTrim=X7",
        "BMW i4": "/searchnew.aspx?ModelAndTrim=i4",
        "BMW iX": "/searchnew.aspx?ModelAndTrim=iX",
        "BMW M3": "/searchnew.aspx?ModelAndTrim=M3",

    };

        const PreOwnedinventorySlugs = {
        "BMW 3 Series": "/searchused.aspx?ModelAndTrim=330i!335i",
        "BMW 5 Series": "/searchused.aspx?ModelAndTrim=530e!530i!540i",
        "BMW X1": "/searchused.aspx?ModelAndTrim=X1",
        "BMW X3": "/searchused.aspx?ModelAndTrim=X3",
        "BMW X5": "/searchused.aspx?ModelAndTrim=X5",
        "BMW X7": "/searchused.aspx?ModelAndTrim=X7",
        "BMW i4": "/searchused.aspx?ModelAndTrim=i4",
        "BMW iX": "/searchused.aspx?ModelAndTrim=iX",
        "BMW M3": "/searchused.aspx?ModelAndTrim=M3",

    };

    const questions = [
      { key: "family", text: "Do you have a family?", options: ["Yes", "No"] },
      { key: "usage", text: "How do you primarily plan to use your vehicle?", options: ["Work Commute", "Adventure / Travel", "Weekend fun"] },
      { key: "priority", text: "What is most important to you?", options: ["Fuel efficiency", "Performance", "Luxury", "Space / Comfort", "Technological Innovation"] },
      { key: "driving", text: "Where do you drive most often?", options: ["City", "Highway / long trips"] },
      { key: "engine", text: "What type of engine do you prefer?", options: ["Gasoline", "Electric", "Hybrid", "Impartial"] }
    ];

    const baseScores = {
      "BMW 3 Series": 0, "BMW 5 Series": 0, "BMW X1": 0, "BMW X3": 0,
      "BMW X5": 0, "BMW X7": 0, "BMW i4": 0, "BMW iX": 0, "BMW M3": 0
    };

    const form = document.getElementById("quiz-form");
    questions.forEach(q => {
      const div = document.createElement("div");
      div.className = "question-block";
      div.innerHTML = `
        <label for="${q.key}">${q.text}</label><br>
        <select id="${q.key}" name="${q.key}" required>
          <option value="" disabled selected>Select an option</option>
          ${q.options.map(opt => `<option value="${opt}">${opt}</option>`).join("")}
        </select>
        <br><br>
      `;
      form.appendChild(div);
    });

    document.getElementById("submit-btn").addEventListener("click", () => {
      const answers = {};
      let allAnswered = true;

      questions.forEach(q => {
        const value = document.getElementById(q.key).value;
        if (!value) allAnswered = false;
        answers[q.key] = value;
      });

      const allAnswersDiv = document.getElementById("allAnswers");

      if (!allAnswered) {
        allAnswersDiv.innerHTML = `<h3 style="color: #ff2c2c;">Please answer all questions before submitting.</h3>`;
        return;
      }

      allAnswersDiv.innerHTML = "";

      const result = recommendCar(answers);

      allAnswersDiv.innerHTML = `
        <h2>Your Ideal BMW</h2>
        <p>Based on your answers, your perfect BMW match is:</p>
        <strong style="color:#000000;font-size:2em;">${result}</strong>
        <br><br>
        &nbsp;
        <a id="New-inventory-btn" target="_blank">View Inventory</a>
        <a id="PreOwned-inventory-btn" target="_blank">View Pre-Owned Inventory</a>
        <button onclick="location.reload()">Restart</button>
      `;

      const iframe = document.getElementById("bmw-info");
      const slug = modelSlugs[result];
      iframe.src = "https://www.bmwpalmsprings.com" + slug;

      const NewinventoryBtn = document.getElementById("New-inventory-btn");
      const NewinventoryPg = modelSlugs[result];
      NewinventoryBtn.href = "https://www.bmwpalmsprings.com" + NewinventoryPg;

      const PreOwnedinventoryBtn = document.getElementById("PreOwned-inventory-btn");
      const PreOwnedinventoryPg = PreOwnedinventorySlugs[result];
      PreOwnedinventoryBtn.href = "https://www.bmwpalmsprings.com" + PreOwnedinventoryPg;
    });

    function recommendCar(answers) {
      const s = { ...baseScores };

      if (answers.family === "Yes") {
        s["BMW X3"] += 2; s["BMW X1"] += 2; s["BMW X5"] += 3; s["BMW X7"] += 2; s["BMW iX"] += 2;
      } else {
        s["BMW 3 Series"] += 4; s["BMW M3"] += 2; s["BMW i4"] += 2; s["BMW 5 Series"] += 3;
      }

      if (answers.usage === "Work Commute") {
        s["BMW 3 Series"] += 2; s["BMW i4"] += 3; s["BMW X3"] += 3; s["BMW X1"] += 2; s["BMW 5 Series"] += 2;
      } else if (answers.usage === "Adventure / Travel") {
        s["BMW X5"] += 3; s["BMW iX"] += 2; s["BMW X3"] += 3; s["BMW X7"] += 4;
      } else if (answers.usage === "Weekend fun") {
        s["BMW M3"] += 4; s["BMW 3 Series"] += 1; s["BMW i4"] += 2; s["BMW X3"] += 2; s["BMW 5 Series"] += 2;
      }

      if (answers.priority === "Fuel efficiency") {
        s["BMW i4"] += 3; s["BMW iX"] += 2; s["BMW X1"] += 3; s["BMW 3 Series"] += 3;
      } else if (answers.priority === "Performance") {
        s["BMW M3"] += 4; s["BMW X5"] += 3; s["BMW iX"] += 3; s["BMW i4"] += 2; s["BMW X3"] += 1;
      } else if (answers.priority === "Luxury") {
        s["BMW 5 Series"] += 3; s["BMW X5"] += 2; s["BMW X7"] += 4; s["BMW iX"] += 4;
      } else if (answers.priority === "Space / Comfort") {
        s["BMW X5"] += 3; s["BMW iX"] += 3; s["BMW X7"] += 4; s["BMW 5 Series"] += 2;
      } else if (answers.priority === "Technological Innovation") {
        s["BMW X7"] += 2; s["BMW iX"] += 4; s["BMW i4"] += 3;
      }

      if (answers.driving === "City") {
        s["BMW i4"] += 2; s["BMW 3 Series"] += 3; s["BMW X1"] += 4; s["BMW X3"] += 3;
      } else {
        s["BMW X5"] += 2; s["BMW M3"] += 2; s["BMW X7"] += 4;
      }

      if (answers.engine === "Electric") {
        s["BMW i4"] += 5; s["BMW iX"] += 5;
      } else if (answers.engine === "Hybrid") {
        s["BMW X1"] += 2; s["BMW X3"] += 2; s["BMW X5"] += 2; s["BMW 5 Series"] += 2;
      } else if (answers.engine === "Gasoline") {
        s["BMW i4"] -= 10; s["BMW iX"] -= 10;
      }

      return Object.entries(s).reduce((a, b) => (a[1] > b[1] ? a : b))[0];
    }
});
