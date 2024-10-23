<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tailwind CSS Table</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 p-10">
  <div class="container mx-auto">
    <h1 class="text-2xl font-bold mb-5">Simple Table</h1>
    <table class="min-w-full bg-white border border-gray-300 rounded-lg">
      <thead>
        <tr class="bg-gray-100 border-b border-gray-300">
          <th class="py-3 px-5 text-left">Name</th>
          <th class="py-3 px-5 text-left">Age</th>
          <th class="py-3 px-5 text-left">Occupation</th>
        </tr>
      </thead>
      <tbody>
        <tr class="border-b border-gray-300">
          <td class="py-3 px-5">John Doe</td>
          <td class="py-3 px-5">28</td>
          <td class="py-3 px-5">Software Developer</td>
        </tr>
        <tr class="border-b border-gray-300">
          <td class="py-3 px-5">Jane Smith</td>
          <td class="py-3 px-5">34</td>
          <td class="py-3 px-5">Graphic Designer</td>
        </tr>
        <tr>
          <td class="py-3 px-5">Emily Brown</td>
          <td class="py-3 px-5">22</td>
          <td class="py-3 px-5">Marketing Specialist</td>
        </tr>
      </tbody>
    </table>
  </div>
</body>
</html>
