import math
import tkinter as tk
from tkinter import ttk, messagebox, scrolledtext
from tkinter.font import Font

class MovieRecommendationApp:
    def __init__(self, root):
        self.root = root
        self.root.title("MovieMate - Recommendation System")
        self.root.geometry("900x700")
        self.root.minsize(900, 700)
        
        # Configure Netflix-inspired color scheme
        self.bg_color = "#141414"  # Netflix dark background
        self.accent_color = "#E50914"  # Netflix red
        self.text_color = "#FFFFFF"  # White text
        self.secondary_bg = "#292929"  # Darker gray for contrast
        
        # Apply theme to root
        self.root.configure(bg=self.bg_color)
        
        # Custom fonts
        self.title_font = Font(family="Helvetica", size=16, weight="bold")
        self.subtitle_font = Font(family="Helvetica", size=14, weight="bold")
        self.text_font = Font(family="Helvetica", size=12)
        self.button_font = Font(family="Helvetica", size=12, weight="bold")
        
        # Configure styles
        self.style = ttk.Style()
        self.style.theme_use('clam')  # Use a theme that supports custom styling
        
        # Configure the background for frames
        self.style.configure('TFrame', background=self.bg_color)
        self.style.configure('TLabelframe', background=self.bg_color, foreground=self.text_color)
        self.style.configure('TLabelframe.Label', background=self.bg_color, foreground=self.text_color, font=self.subtitle_font)
        
        # Configure labels
        self.style.configure('TLabel', background=self.bg_color, foreground=self.text_color, font=self.text_font)
        
        # Configure buttons
        self.style.configure('TButton', 
                             background=self.accent_color, 
                             foreground=self.text_color, 
                             font=self.button_font,
                             borderwidth=0)
        self.style.map('TButton', 
                       background=[('active', '#FF0F1A'), ('pressed', '#C70000')])
        
        # Configure combobox
        self.style.configure('TCombobox', 
                            selectbackground=self.accent_color,
                            fieldbackground=self.secondary_bg,
                            background=self.secondary_bg,
                            foreground=self.text_color,
                            arrowcolor=self.text_color,
                            font=self.text_font)
        
        # Configure entry
        self.style.configure('TEntry', 
                            fieldbackground=self.secondary_bg,
                            foreground=self.text_color,
                            insertcolor=self.text_color,
                            font=self.text_font)
        
        # Configure radiobuttons
        self.style.configure('TRadiobutton', 
                           background=self.bg_color,
                           foreground=self.text_color,
                           font=self.text_font)
        
        # Configure notebook (tabs)
        self.style.configure('TNotebook', 
                           background=self.bg_color,
                           tabmargins=[2, 5, 2, 0])
        self.style.configure('TNotebook.Tab', 
                           background=self.secondary_bg,
                           foreground=self.text_color,
                           padding=[20, 10],
                           font=self.text_font)
        self.style.map('TNotebook.Tab', 
                      background=[('selected', self.accent_color)],
                      expand=[('selected', [1, 1, 1, 0])])
        
        # Sample data
        self.user_history = {
            "user1": [("The Shawshank Redemption", 5), ("The Godfather", 4), ("Pulp Fiction", 5), 
                     ("The Dark Knight", 4), ("Fight Club", 3)],
            "user2": [("The Godfather", 5), ("Inception", 5), ("The Matrix", 4), 
                     ("Interstellar", 5), ("The Dark Knight", 5)],
            "user3": [("Pulp Fiction", 5), ("Fight Club", 4), ("Inception", 3), 
                     ("The Matrix", 4), ("Goodfellas", 5)],
            "user4": [("The Shawshank Redemption", 4), ("Forrest Gump", 5), ("The Green Mile", 5),
                     ("Schindler's List", 4), ("The Godfather", 3)]
        }
        
        # App title
        self.header_frame = ttk.Frame(root)
        self.header_frame.pack(fill="x", padx=20, pady=(20, 10))
        
        self.logo_label = tk.Label(self.header_frame, 
                                  text="MovieMate", 
                                  font=("Helvetica", 28, "bold"), 
                                  bg=self.bg_color, 
                                  fg=self.accent_color)
        self.logo_label.pack(side=tk.LEFT)
        
        self.tagline_label = tk.Label(self.header_frame, 
                                     text="Your Personal Movie Recommender", 
                                     font=("Helvetica", 14), 
                                     bg=self.bg_color, 
                                     fg=self.text_color)
        self.tagline_label.pack(side=tk.LEFT, padx=(10, 0), pady=(10, 0))
        
        # Create main content frame to center everything
        self.main_frame = ttk.Frame(root)
        self.main_frame.pack(fill="both", expand=True, padx=40, pady=20)
        
        # Configure main frame to center its content
        self.main_frame.columnconfigure(0, weight=1)
        self.main_frame.rowconfigure(0, weight=1)
        
        # Create tabs
        self.tab_control = ttk.Notebook(self.main_frame)
        self.tab_control.grid(row=0, column=0, sticky="nsew")
        
        self.tab1 = ttk.Frame(self.tab_control)
        self.tab2 = ttk.Frame(self.tab_control)
        self.tab3 = ttk.Frame(self.tab_control)
        
        self.tab_control.add(self.tab1, text="Get Recommendations")
        self.tab_control.add(self.tab2, text="Add/Edit User")
        self.tab_control.add(self.tab3, text="Browse Movies")
        
        # Setup each tab
        self.setup_recommendations_tab()
        self.setup_user_tab()
        self.setup_movie_tab()
        
        # Set up footer
        self.footer_frame = ttk.Frame(root)
        self.footer_frame.pack(fill="x", padx=20, pady=10)
        
        self.footer_label = tk.Label(self.footer_frame, 
                                    text="© 2025 MovieMate - Personalized Recommendations", 
                                    font=("Helvetica", 10), 
                                    bg=self.bg_color, 
                                    fg="#8C8C8C")
        self.footer_label.pack(side=tk.RIGHT)
    
    def create_scrolled_text(self, parent):
        """Create a custom styled ScrolledText widget"""
        text = scrolledtext.ScrolledText(parent, 
                                        wrap=tk.WORD, 
                                        bg=self.secondary_bg, 
                                        fg=self.text_color, 
                                        insertbackground=self.text_color,
                                        font=self.text_font,
                                        borderwidth=0,
                                        highlightthickness=1,
                                        highlightcolor=self.accent_color,
                                        highlightbackground=self.accent_color)
        return text
    
    def setup_recommendations_tab(self):
        # Center frame
        center_frame = ttk.Frame(self.tab1)
        center_frame.pack(fill="both", expand=True)
        center_frame.columnconfigure(0, weight=1)
        
        frame = ttk.LabelFrame(center_frame, text="Movie Recommendations")
        frame.grid(row=0, column=0, padx=10, pady=10, sticky="nsew")
        frame.columnconfigure(0, weight=1)
        frame.columnconfigure(1, weight=1)
        frame.columnconfigure(2, weight=1)
        
        # User selection
        user_select_frame = ttk.Frame(frame)
        user_select_frame.grid(row=0, column=0, columnspan=3, padx=10, pady=20, sticky="nsew")
        user_select_frame.columnconfigure(1, weight=1)
        
        ttk.Label(user_select_frame, text="Select User:").grid(row=0, column=0, padx=10, pady=10, sticky="e")
        self.user_var = tk.StringVar()
        self.user_combo = ttk.Combobox(user_select_frame, textvariable=self.user_var, state="readonly", width=30)
        self.user_combo['values'] = list(self.user_history.keys())
        self.user_combo.grid(row=0, column=1, padx=10, pady=10, sticky="ew")
        
        # Button to get recommendations
        recommend_button = ttk.Button(user_select_frame, text="Get Recommendations", command=self.get_recommendations)
        recommend_button.grid(row=0, column=2, padx=10, pady=10, sticky="w")
        
        # Container for the two text areas
        text_container = ttk.Frame(frame)
        text_container.grid(row=1, column=0, columnspan=3, padx=10, pady=10, sticky="nsew")
        text_container.columnconfigure(0, weight=1)
        text_container.columnconfigure(1, weight=1)
        text_container.rowconfigure(0, weight=0)
        text_container.rowconfigure(1, weight=1)
        
        # Frame for user's movies
        ttk.Label(text_container, text="Your Movies", font=self.subtitle_font).grid(row=0, column=0, padx=10, pady=(0, 5), sticky="w")
        
        self.user_movies_text = self.create_scrolled_text(text_container)
        self.user_movies_text.grid(row=1, column=0, padx=10, pady=5, sticky="nsew")
        
        # Frame for recommendations
        ttk.Label(text_container, text="Recommended For You", font=self.subtitle_font).grid(row=0, column=1, padx=10, pady=(0, 5), sticky="w")
        
        self.recommendations_text = self.create_scrolled_text(text_container)
        self.recommendations_text.grid(row=1, column=1, padx=10, pady=5, sticky="nsew")
        
        # Configure weights
        center_frame.rowconfigure(0, weight=1)
        frame.rowconfigure(1, weight=1)
    
    def setup_user_tab(self):
        # Center frame
        center_frame = ttk.Frame(self.tab2)
        center_frame.pack(fill="both", expand=True)
        center_frame.columnconfigure(0, weight=1)
        
        frame = ttk.LabelFrame(center_frame, text="Add/Edit User")
        frame.grid(row=0, column=0, padx=10, pady=10, sticky="nsew")
        
        # Center the content within the frame
        frame.columnconfigure(0, weight=1)
        frame.columnconfigure(1, weight=2)
        frame.columnconfigure(2, weight=1)
        
        content_frame = ttk.Frame(frame)
        content_frame.grid(row=0, column=1, padx=10, pady=10, sticky="nsew")
        
        # User selection/creation
        ttk.Label(content_frame, text="User ID:").grid(row=0, column=0, padx=10, pady=10, sticky="w")
        self.new_user_var = tk.StringVar()
        self.new_user_entry = ttk.Entry(content_frame, textvariable=self.new_user_var, width=30)
        self.new_user_entry.grid(row=0, column=1, padx=10, pady=10, sticky="ew")
        
        # Movie entry
        ttk.Label(content_frame, text="Movie Title:").grid(row=1, column=0, padx=10, pady=10, sticky="w")
        self.movie_var = tk.StringVar()
        self.movie_entry = ttk.Entry(content_frame, textvariable=self.movie_var, width=30)
        self.movie_entry.grid(row=1, column=1, padx=10, pady=10, sticky="ew")
        
        # Rating
        ttk.Label(content_frame, text="Rating:").grid(row=2, column=0, padx=10, pady=10, sticky="w")
        self.rating_var = tk.IntVar(value=5)
        rating_frame = ttk.Frame(content_frame)
        rating_frame.grid(row=2, column=1, padx=10, pady=10, sticky="w")
        
        for i in range(1, 6):
            rb = ttk.Radiobutton(rating_frame, text=str(i), variable=self.rating_var, value=i)
            rb.pack(side=tk.LEFT, padx=15, pady=5)
        
        # Add button
        add_button = ttk.Button(content_frame, text="Add Rating", command=self.add_rating)
        add_button.grid(row=3, column=0, columnspan=2, padx=10, pady=20)
        
        # User ratings display
        ttk.Label(content_frame, text="Current User Ratings:", font=self.subtitle_font).grid(
            row=4, column=0, columnspan=2, padx=10, pady=(20,5), sticky="w")
        
        self.user_ratings_text = self.create_scrolled_text(content_frame)
        self.user_ratings_text.grid(row=5, column=0, columnspan=2, padx=10, pady=5, sticky="nsew")
        self.user_ratings_text.config(height=12)
        
        # Configure weights
        center_frame.rowconfigure(0, weight=1)
        frame.rowconfigure(0, weight=1)
        content_frame.rowconfigure(5, weight=1)
        content_frame.columnconfigure(1, weight=1)
    
    def setup_movie_tab(self):
        # Center frame
        center_frame = ttk.Frame(self.tab3)
        center_frame.pack(fill="both", expand=True)
        center_frame.columnconfigure(0, weight=1)
        
        frame = ttk.LabelFrame(center_frame, text="Browse Movies")
        frame.grid(row=0, column=0, padx=10, pady=10, sticky="nsew")
        
        # Center the content
        frame.columnconfigure(0, weight=1)
        frame.columnconfigure(1, weight=2)
        frame.columnconfigure(2, weight=1)
        
        content_frame = ttk.Frame(frame)
        content_frame.grid(row=0, column=1, padx=10, pady=10, sticky="nsew")
        content_frame.columnconfigure(0, weight=1)
        
        # Display all unique movies in the system
        ttk.Label(content_frame, text="All Movies in System:", font=self.subtitle_font).grid(
            row=0, column=0, padx=10, pady=10, sticky="w")
        
        self.movies_text = self.create_scrolled_text(content_frame)
        self.movies_text.grid(row=1, column=0, padx=10, pady=10, sticky="nsew")
        
        # Update movie list
        self.update_movie_list()
        
        # Configure weights
        center_frame.rowconfigure(0, weight=1)
        frame.rowconfigure(0, weight=1)
        content_frame.rowconfigure(1, weight=1)
    
    def cosine_similarity(self, user1_ratings, user2_ratings):
        """Calculate cosine similarity between two users based on their movie ratings."""
        user1_dict = dict(user1_ratings)
        user2_dict = dict(user2_ratings)
        
        common_movies = set(user1_dict.keys()) & set(user2_dict.keys())
        
        if not common_movies:
            return 0
        
        dot_product = sum(user1_dict[movie] * user2_dict[movie] for movie in common_movies)
        
        magnitude1 = math.sqrt(sum(rating ** 2 for rating in user1_dict.values()))
        magnitude2 = math.sqrt(sum(rating ** 2 for rating in user2_dict.values()))
        
        if magnitude1 == 0 or magnitude2 == 0:
            return 0
        
        return dot_product / (magnitude1 * magnitude2)
    
    def recommend_movies(self, target_user):
        """Generate movie recommendations for the target user."""
        if target_user not in self.user_history:
            return []
            
        similarities = {}
        for user, ratings in self.user_history.items():
            if user != target_user:
                similarities[user] = self.cosine_similarity(self.user_history[target_user], ratings)
        
        sorted_similarities = sorted(similarities.items(), key=lambda item: item[1], reverse=True)
        top_similar_users = sorted_similarities[:3]  # Top 3 users
        
        target_movies = set(movie for movie, _ in self.user_history[target_user])
        
        recommendations = {}
        for user, similarity in top_similar_users:
            if similarity <= 0:
                continue
                
            for movie, rating in self.user_history[user]:
                if movie not in target_movies:
                    if movie in recommendations:
                        recommendations[movie] += rating * similarity
                    else:
                        recommendations[movie] = rating * similarity
        
        sorted_recommendations = sorted(recommendations.items(), key=lambda item: item[1], reverse=True)
        return sorted_recommendations
    
    def get_recommendations(self):
        """Handle recommendation button click."""
        user = self.user_var.get()
        if not user:
            messagebox.showwarning("Warning", "Please select a user")
            return
            
        # Display user's movies
        self.user_movies_text.delete(1.0, tk.END)
        if user in self.user_history:
            for movie, rating in self.user_history[user]:
                stars = "★" * rating + "☆" * (5 - rating)
                self.user_movies_text.insert(tk.END, f"{movie}\n{stars}\n\n")
        
        # Get and display recommendations
        recommendations = self.recommend_movies(user)
        self.recommendations_text.delete(1.0, tk.END)
        
        if not recommendations:
            self.recommendations_text.insert(tk.END, "No recommendations found.")
            return
            
        for movie, score in recommendations:
            # Normalize score for display (between 1-5)
            normalized_score = min(5, max(1, round(score, 1)))
            stars = "★" * int(normalized_score) 
            if normalized_score % 1 >= 0.5:  # Add half star if needed
                stars += "✬"
            stars += "☆" * (5 - int(normalized_score) - (1 if normalized_score % 1 >= 0.5 else 0))
            
            self.recommendations_text.insert(tk.END, f"{movie}\n{stars} ({normalized_score})\n\n")
    
    def add_rating(self):
        """Add a movie rating for a user."""
        user = self.new_user_var.get().strip()
        movie = self.movie_var.get().strip()
        rating = self.rating_var.get()
        
        if not user or not movie:
            messagebox.showwarning("Warning", "Please enter both user ID and movie title")
            return
        
        # Create user if doesn't exist
        if user not in self.user_history:
            self.user_history[user] = []
            # Update user dropdown
            self.user_combo['values'] = list(self.user_history.keys())
        
        # Check if movie already rated
        movie_exists = False
        for i, (m, r) in enumerate(self.user_history[user]):
            if m == movie:
                # Update existing rating
                self.user_history[user][i] = (movie, rating)
                movie_exists = True
                break
                
        if not movie_exists:
            # Add new rating
            self.user_history[user].append((movie, rating))
        
        # Success message with Netflix-inspired styling
        self.show_custom_message("Rating Added", f"{movie} rated {rating} stars")
        
        # Clear entries
        self.movie_var.set("")
        
        # Update displays
        self.update_user_ratings()
        self.update_movie_list()
    
    def show_custom_message(self, title, message):
        """Show a custom-styled message box"""
        msg_window = tk.Toplevel(self.root)
        msg_window.title(title)
        msg_window.configure(bg=self.bg_color)
        msg_window.geometry("300x150")
        
        # Center the window
        msg_window.geometry("+%d+%d" % (
            self.root.winfo_rootx() + self.root.winfo_width()/2 - 150,
            self.root.winfo_rooty() + self.root.winfo_height()/2 - 75))
        
        # Make window modal
        msg_window.grab_set()
        msg_window.transient(self.root)
        
        # Add message
        msg_label = tk.Label(msg_window, 
                            text=message, 
                            bg=self.bg_color, 
                            fg=self.text_color, 
                            font=self.text_font,
                            wraplength=250)
        msg_label.pack(expand=True, fill="both", padx=20, pady=(20, 10))
        
        # Add OK button
        ok_button = tk.Button(msg_window, 
                             text="OK", 
                             bg=self.accent_color, 
                             fg=self.text_color, 
                             font=self.button_font,
                             relief="flat",
                             bd=0,
                             padx=20, pady=5,
                             command=msg_window.destroy)
        ok_button.pack(pady=(0, 20))
        
        # Ensure the window closes properly
        msg_window.protocol("WM_DELETE_WINDOW", msg_window.destroy)
        
        # Wait for the window to be closed
        self.root.wait_window(msg_window)
    
    def update_user_ratings(self):
        """Update the display of current user ratings."""
        user = self.new_user_var.get().strip()
        self.user_ratings_text.delete(1.0, tk.END)
        
        if user in self.user_history:
            for movie, rating in self.user_history[user]:
                stars = "★" * rating + "☆" * (5 - rating)
                self.user_ratings_text.insert(tk.END, f"{movie}\n{stars}\n\n")
    
    def update_movie_list(self):
        """Update the display of all movies in the system."""
        all_movies = set()
        for ratings in self.user_history.values():
            for movie, _ in ratings:
                all_movies.add(movie)
        
        self.movies_text.delete(1.0, tk.END)
        for movie in sorted(all_movies):
            self.movies_text.insert(tk.END, f"• {movie}\n")

if __name__ == "__main__":
    root = tk.Tk()
    app = MovieRecommendationApp(root)
    root.mainloop()
