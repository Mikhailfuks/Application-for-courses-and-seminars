using System;
using System.Collections.Generic;

namespace CourseManagement
{
    class Program
    {
        public class Course
        {
            public string Title { get; set; }
            public string Description { get; set; }
            public List<string> EnrolledStudents { get; set; }

            public Course(string title, string description)
            {
                Title = title;
                Description = description;
                EnrolledStudents = new List<string>();
            }

            public void EnrollStudent(string studentName)
            {
                EnrolledStudents.Add(studentName);
            }

            public override string ToString()
            {
                return $"{Title}: {Description}, Registered Students: {EnrolledStudents.Count}";
            }
        }

        static List<Course> courses = new List<Course>();

        static void Main(string[] args)
        {
            string command;

            do
            {
                Console.WriteLine("Введите команду: add, list, enroll, exit");
                command = Console.ReadLine();

                switch (command)
                {
                    case "add":
                        AddCourse();
                        break;
                    case "list":
                        ListCourses();
                        break;
                    case "enroll":
                        EnrollStudent();
                        break;
                }
            } while (command != "exit");
        }

        static void AddCourse()
        {
            Console.Write("Введите название курса: ");
            string title = Console.ReadLine();

            Console.Write("Введите описание курса: ");
            string description = Console.ReadLine();

            Course newCourse = new Course(title, description);
            courses.Add(newCourse);

            Console.WriteLine("Курс добавлен.");
        }

        static void ListCourses()
        {
            Console.WriteLine("Доступные курсы:");
            foreach (var course in courses)
            {
                Console.WriteLine(course);
            }
        }

        static void EnrollStudent()
        {
            Console.Write("Введите название курса: ");
            string courseTitle = Console.ReadLine();
            var course = courses.Find(c => c.Title.Equals(courseTitle, StringComparison.OrdinalIgnoreCase));

            if (course != null)
            {
                Console.Write("Введите имя студента: ");
                string studentName = Console.ReadLine();
                course.EnrollStudent(studentName);
                Console.WriteLine("Студент зарегистрирован на курс.");
            }
            else
            {
                Console.WriteLine("Курс не найден.");
            }
        }
    }
}
